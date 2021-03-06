# Generate compile time constant class from xsd using jaxb
```xml
 <build>
        <defaultGoal>install</defaultGoal>
    <!--start plugin important-->
        <pluginManagement>
            <plugins>
                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-compiler-plugin</artifactId>
                    <configuration>
                        <source>1.8</source>
                        <target>1.8</target>
                    </configuration>
                </plugin>
            </plugins>
        </pluginManagement>
        <plugins>
            <plugin>
                <groupId>org.codehaus.mojo</groupId>
                <artifactId>jaxb2-maven-plugin</artifactId>
                <version>2.5.0</version>
                <executions>
                    <execution>
                        <id>xjc</id>
                        <goals>
                            <goal>xjc</goal>
                        </goals>
                    </execution>
                </executions>
                <configuration>

                    <!-- Define the directory where we should find the DTD files -->
                    <sources>
                        <source>src/main/resources/xsd</source>
                    </sources>
                    <!-- Set the package of the generated code -->
                    <packageName>com.example.myschema</packageName>
                    <outputDirectory>target/generate-sources/jaxb</outputDirectory>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.codehaus.mojo</groupId>
                <artifactId>build-helper-maven-plugin</artifactId>
                <executions>
                    <execution>
                        <goals>
                            <goal>add-source</goal>
                        </goals>
                        <configuration>
                            <sources>
                                <source>target/generated-sources</source>
                            </sources>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>


    </build>
```
#### sample xsd 
```xml
<?xml version="1.0"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"
           targetNamespace="http://widget.com/types/widgetTypes"
           xmlns:jaxb="http://java.sun.com/xml/ns/jaxb"
           jaxb:version="2.0">
    <xs:annotation>
        <xs:appinfo>
            <jaxb:globalBindings fixedAttributeAsConstantProperty="true" />
        </xs:appinfo>
    </xs:annotation>
    <xs:complexType name="Employee">
        <xs:attribute name="firstname" type="xs:string" fixed="Srikanth"/>
        <xs:attribute name="lastname" type="xs:string" fixed="Dannarapu"/>
        <xs:attribute name="email" type="xs:string" fixed="Srikant.dannarapu@gmail.com"/>
    </xs:complexType>

</xs:schema>
```
#### Following java class is generated 

```java
@XmlAccessorType(XmlAccessType.FIELD)
@XmlType(name = "Employee")
public class Employee {

    /**
     * 
     * 
     */
    @XmlAttribute(name = "firstname")
    public final static String FIRSTNAME = "Srikanth";
}
```