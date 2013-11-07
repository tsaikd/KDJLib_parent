KDJLib_parent
=============

KDJLib maven base pom


Install
=======
* Add to project pom.xml
```
<project>
	...

	<parent>
		<groupId>org.tsaikd.java</groupId>
		<artifactId>KDJLib_parent</artifactId>
		<version>0.0.11</version>
	</parent>

	<repositories>
		<repository>
			<id>tsaikd</id>
			<name>tsaikd maven repository</name>
			<url>http://www.tsaikd.org/nexus/content/repositories/releases/</url>
		</repository>
	</repositories>

	...
</project>
```

* $HOME/settings.xml
```
<settings>
        <profiles>
                <profile>
                        <id>deploy-release</id>
                        <properties>
                                <altDeploymentRepository>nexus::default::http://NEXUS-HOST:NEXUS-PORT/nexus/content/repositories/releases</altDeploymentRepository>
                        </properties>
                </profile>
                <profile>
                        <id>deploy-snapshot</id>
                        <properties>
                                <altDeploymentRepository>nexus::default::http://NEXUS-HOST:NEXUS-PORT/nexus/content/repositories/snapshots</altDeploymentRepository>
                        </properties>
                </profile>
                <profile>
                        <id>deploy-tomcat</id>
                        <properties>
                                <tomcat-manager-url>http://TOMCAT-HOST:TOMCAT-PORT/manager/text</tomcat-manager-url>
                        </properties>
                </profile>
        </profiles>
        <servers>
                <server>
                        <id>nexus</id>
                        <username>NEXUS-DEPLOY-USER</username>
                        <password>NEXUS-DEPLOY-PASS</password>
                </server>
                <server>
                        <id>tomcat</id>
                        <username>TOMCAT-DEPLOY-USER</username>
                        <password>TOMCAT-DEPLOY-PASS</password>
                </server>
        </servers>
</settings>
```
* Replace
	* NEXUS-HOST
	* NEXUS-PORT
	* TOMCAT-HOST
	* TOMCAT-PORT
	* NEXUS-DEPLOY-USER
	* NEXUS-DEPLOY-PASS
	* TOMCAT-DEPLOY-USER
	* TOMCAT-DEPLOY-PASS

Usage
=====
* package

```
mvn clean test package
```

* deploy snapshot: (altDeploymentRepository)

```
mvn clean test package deploy -P deploy-snapshot -P deploy-source -U
```

* deploy release: (altDeploymentRepository)

```
mvn clean test package deploy -P deploy-release -P deploy-source -U
```

* deploy tomcat: (tomcat-manager-url, tomcat-server-id, tomcat-deploy-path)

```
mvn clean test package tomcat:deploy -P deploy-tomcat -U
```

* package single jar: (mainClass)

```
mvn clean test package -P deploy-single -U
```
