# Java-Agent-quickstart

在Java中添加数据探针通常涉及使用Java Agent技术，这是一种在JVM启动时或运行时动态插入代码的方法，不需要修改应用程序的源代码。以下是一个简单的Java Agent实现的quickstart例子，包括创建Agent和使用它来监控一个简单Java应用程序的步骤。

### 步骤1: 创建Java Agent

首先，你需要创建一个Java Agent。这个Agent将在Java应用程序启动时被加载，并可以修改类的字节码，插入我们需要的监控代码。

1. **创建Maven项目**：使用IDE（如IntelliJ IDEA）或命令行创建一个新的Maven项目。
2. **添加依赖**：在`pom.xml`文件中添加必要的依赖。这通常包括`asm`或`javassist`，这些库帮助操作字节码。

   ```xml
   <dependencies>
       <dependency>
           <groupId>org.javassist</groupId>
           <artifactId>javassist</artifactId>
           <version>3.28.0-GA</version>
       </dependency>
   </dependencies>
   ```

3. **编写Agent类**：创建一个新的Java类，实现`premain`方法。这个方法是Agent的入口点。

   ```java
   import java.lang.instrument.Instrumentation;

   public class MyAgent {
       public static void premain(String agentArgs, Instrumentation inst) {
           System.out.println("MyAgent is running");
           // 这里可以添加更多的字节码操作
       }
   }
   ```

4. **配置MANIFEST.MF**：在`src/main/resources/META-INF/MANIFEST.MF`中添加以下内容：

   ```
   Manifest-Version: 1.0
   Premain-Class: MyAgent
   Can-Redefine-Classes: true
   Can-Retransform-Classes: true
   ```

5. **打包Agent**：使用Maven打包你的项目。生成的JAR文件将用作Java Agent。

   ```bash
   mvn clean package
   ```

### 步骤2: 创建测试Java应用

创建一个简单的Java应用程序来使用这个Agent。

1. **创建Java类**：

   ```java
   public class MyApp {
       public static void main(String[] args) {
           System.out.println("Hello, World!");
       }
   }
   ```

2. **编译应用**：

   ```bash
   javac MyApp.java
   ```

### 步骤3: 运行应用并加载Agent

使用以下命令运行你的应用程序，并通过`-javaagent`参数指定你的Agent JAR文件。

```bash
java -javaagent:path_to_your_agent.jar -jar MyApp.jar
```

替换`path_to_your_agent.jar`为你的Agent JAR文件的实际路径。运行这个命令后，你应该能看到Agent打印的消息和应用程序的输出。

这个quickstart例子展示了如何创建和使用Java Agent来在运行时动态添加数据探针，而无需修改应用程序的源代码。你可以根据需要扩展Agent的功能，比如添加更复杂的数据收集和处理逻辑[5][6][8][13][14][15][16][18][19][20].

Citations:
[1] https://skywalking.apache.org/zh/2022-04-19-how-to-use-the-java-agent-injector/
[2] https://blog.51cto.com/panyujie/8688866
[3] https://www.cnblogs.com/liboware/p/15090408.html
[4] https://yaoyuanyy.github.io/2020/03/10/%E4%B8%8D%E7%9F%A5%E9%81%93javaagent%E6%98%AF%E4%BB%80%E4%B9%88%EF%BC%8C%E8%BF%90%E8%A1%8C%E4%B8%8Bhello%20world%E5%B0%B1%E7%9F%A5%E9%81%93%E4%BA%86/
[5] https://juejin.cn/post/7086026013498408973
[6] https://blog.csdn.net/qq_39956994/article/details/127783067
[7] https://www.zhihu.com/account/unhuman?need_login=true&type=S6E3V1
[8] https://www.cnblogs.com/jackion5/p/10679728.html
[9] https://docs.unity.cn/cn/tuanjiemanual/Manual/AutoStreamingDemo.html
[10] https://www.zhihu.com/question/545762884
[11] https://billtian.github.io/digoal.blog/year-archive/
[12] https://github.com/owen800q/Awesome-Stars
[13] https://blog.csdn.net/Quarrie/article/details/103109274
[14] https://blog.csdn.net/JKX_geek/article/details/104715719
[15] https://jb51.net/article/251757.htm
[16] https://blog.csdn.net/ory001/article/details/118676155
[17] https://www.alibabacloud.com/zh/news/product/arms-agent-for-java-v290-released-ivw?_p_lc=1
[18] https://developer.baidu.com/article/details/2976136
[19] https://blog.51cto.com/knifeedge/5010801
[20] https://blog.51cto.com/u_16175453/7862099
