# 编译 & 构建
1. 以下操作无特殊说明，均在终端中执行；
2. SDKMAN 使用 JDK 8；
2. build.gradle 文件中，将 maven 仓库源替换为阿里源；
3. 参考文件 [https://github.com/spring-projects/spring-framework/blob/4.1.x/import-into-idea.md](https://github.com/spring-projects/spring-framework/blob/4.1.x/import-into-idea.md)
执行命令：`./gradlew cleanIdea :spring-oxm:compileTestJava`
4. 参考文件 [https://github.com/spring-projects/spring-framework/blob/4.1.x/README.md](https://github.com/spring-projects/spring-framework/blob/4.1.x/README.md)
执行如下命令：
```bash
./gradlew install
./gradlew build
```
5. 执行命令 `./gradlew tasks` 查看支持的任务；
6. 执行如下任务：`./gradlew idea`；
7. 使用 IDEA 打开项目；