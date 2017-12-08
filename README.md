Maven java application with slf4j-logger jar

A simple java maven application to include sl4j_logger jar during runtime.

****************************************************************************************************************************
Steps to run the java application : 
****************************************************************************************************************************

1. Using maven shade plugin to add 3rd party jars into application jar during runtime :
    
i) For building the jar : Use command : mvn clean package

ii) Add plugin :
	
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.1</version>
            <executions>
                <execution>
                    <phase>package</phase>
                    <goals>
                        <goal>shade</goal>
                    </goals>
                    <configuration>
                        <transformers>
                            <transformer
                                implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                                <mainClass>com.emc.test_logger.App</mainClass>
                            </transformer>
                        </transformers>
                    </configuration>
                </execution>
            </executions>
        </plugin>
								
2. 	Using maven-jar & maven-assembly jar plugins to add 3rd party jars into application jar during runtime:
	
	i) For building the jar : use command : mvn clean compile assembly:single
	
	ii) Add plugin :
	
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-jar-plugin</artifactId>
				<version>3.0.2</version>
				<configuration>
					<archive>
						<manifest>
							<addClasspath>true</addClasspath>
							<classpathPrefix>lib/</classpathPrefix>
							<mainClass>com.emc.test_logger.App</mainClass>
						</manifest>
					</archive>
				</configuration>
			</plugin>
			<plugin>
				<artifactId>maven-assembly-plugin</artifactId>
				<configuration>
					<archive>
						<manifest>
							<mainClass>com.emc.test_logger.App</mainClass>
						</manifest>
					</archive>
					<descriptorRefs>
						<descriptorRef>jar-with-dependencies</descriptorRef>
					</descriptorRefs>
				</configuration>
			</plugin>

****************************************************************************************************************************								
