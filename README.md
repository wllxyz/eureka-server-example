# eureka-server-example
eureka-server sample

Eureka Server:

	1. 项目依赖

		1. <?xml version="1.0" encoding="UTF-8"?>
		2. <project xmlns="http://maven.apache.org/POM/4.0.0"; xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance";
		3.     xsi:schemaLocation="http://maven.apache.org/POM/4.0.0http://maven.apache.org/xsd/maven-4.0.0.xsd">;
		4.     <modelVersion>4.0.0</modelVersion>
		5.     <groupId>com.example</groupId>
		6.     <artifactId>eureka-client</artifactId>
		7.     <version>0.0.1-SNAPSHOT</version>
		8.     <packaging>jar</packaging>
		9.     <parent>
		10.         <groupId>org.springframework.boot</groupId>
		11.         <artifactId>spring-boot-starter-parent</artifactId>
		12.         <version>1.5.9.RELEASE</version>
		13.         <relativePath/> <!-- lookup parent from repository -->
		14.     </parent>
		15.     <properties>
		16.         <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		17.         <java.version>1.8</java.version>
		18.     </properties>
		19.     <dependencies>
		20.         <dependency>
		21.             <groupId>org.springframework.cloud</groupId>
		22.             <artifactId>spring-cloud-starter-eureka</artifactId>
		23.         </dependency>
		24.         <dependency>
		25.             <groupId>org.springframework.boot</groupId>
		26.             <artifactId>spring-boot-starter-test</artifactId>
		27.             <scope>test</scope>
		28.         </dependency>
		29.         <dependency>
		30.             <groupId>org.springframework.cloud</groupId>
		31.             <artifactId>spring-cloud-starter-eureka-server</artifactId>
		32.             <scope>test</scope>
		33.         </dependency>
		34.     </dependencies>
		35.     <dependencyManagement>
		36.         <dependencies>
		37.             <dependency>
		38.                 <groupId>org.springframework.cloud</groupId>
		39.                 <artifactId>spring-cloud-dependencies</artifactId>
		40.                 <version>Edgware.RELEASE</version>
		41.                 <type>pom</type>
		42.                 <scope>import</scope>
		43.             </dependency>
		44.         </dependencies>
		45.     </dependencyManagement>
		46.     <build>
		47.         <plugins>
		48.             <plugin>
		49.                 <groupId>org.springframework.boot</groupId>
		50.                 <artifactId>spring-boot-maven-plugin</artifactId>
		51.             </plugin>
		52.         </plugins>
		53.     </build>
		54.     <repositories>
		55.         <repository>
		56.             <id>spring-snapshots</id>
		57.             <name>Spring Snapshots</name>
		58.             <url>https://repo.spring.io/libs-snapshot</url>;
		59.             <snapshots>
		60.                 <enabled>true</enabled>
		61.             </snapshots>
		62.         </repository>
		63.     </repositories>
		64. </project>


            说明：
                spring-boot-start-parent简化spring-boot项目依赖

	1.     <parent>
	2.         <groupId>org.springframework.boot</groupId>
	3.         <artifactId>spring-boot-starter-parent</artifactId>
	4.         <version>1.5.9.RELEASE</version>
	5.         <relativePath/> <!-- lookup parent from repository -->
	6.     </parent>


                添加spring-cloud-starter-eureka公共依赖
                

	1.         <dependency>
	2.             <groupId>org.springframework.cloud</groupId>
	3.             <artifactId>spring-cloud-starter-eureka</artifactId>
	4.         </dependency>


                添加spring-cloud-dependencies公共依赖


	1.             <dependency>
	2.                 <groupId>org.springframework.cloud</groupId>
	3.                 <artifactId>spring-cloud-dependencies</artifactId>
	4.                 <version>Edgware.RELEASE</version>
	5.                 <type>pom</type>
	6.                 <scope>import</scope>
	7.             </dependency>


                spring-boot项目打包插件


	1.     <build>
	2.         <plugins>
	3.             <plugin>
	4.                 <groupId>org.springframework.boot</groupId>
	5.                 <artifactId>spring-boot-maven-plugin</artifactId>
	6.             </plugin>
	7.         </plugins>
	8.     </build>

            

	2. 项目代码

            package hello;
            import org.springframework.boot.SpringApplication;
            import org.springframework.boot.autoconfigure.SpringBootApplication;
            import org.springframework.cloud.netflix.eureka.server.EnableEurekaServer;
            @EnableEurekaServer
            @SpringBootApplication
            public class EurekaServiceApplication {
    
                public static void main(String[] args) {
                    SpringApplication.run(EurekaServiceApplication.class, args);
                }
            }

        说明：和普通的spring-boot服务相比，只多了一行注解@EnableEurekaServer


	3. 项目配置


        server.port=8761
        eureka.client.register-with-eureka=false
        eureka.client.fetch-registry=false
        logging.level.com.netflix.eureka=OFF
        logging.level.com.netflix.discovery=OFF

        eureka server默认监听端口是8761，客户端注册也是默认连这个端口。
        服务端需要关闭注册和从注册中心订阅的行为。
