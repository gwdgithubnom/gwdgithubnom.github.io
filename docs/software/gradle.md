## 基础命令

### 构建相关

```bash
# 清理构建目录
./gradlew clean

# 执行构建（编译、测试、打包）
./gradlew build

# 仅编译项目
./gradlew compileJava

# 仅编译测试代码
./gradlew compileTestJava

# 运行测试
./gradlew test

# 生成 JAR 包
./gradlew jar

# 生成包含所有依赖的 fat JAR
./gradlew shadowJar
```

### 项目信息

```bash
# 显示项目基本信息
./gradlew projects

# 显示项目依赖树
./gradlew dependencies

# 显示特定配置的依赖
./gradlew dependencies --configuration compileClasspath
./gradlew dependencies --configuration testCompileClasspath

# 显示项目属性
./gradlew properties

# 显示所有可用任务
./gradlew tasks

# 显示帮助信息
./gradlew help
```

## 应用插件相关命令

### Java/Application 插件

```bash
# 运行应用程序（需要 application 插件）
./gradlew run

# 显示主类信息
./gradlew mainClassName

# 创建分发包（包含启动脚本）
./gradlew distTar
./gradlew distZip
```

### Spring Boot 插件

```bash
# 启动 Spring Boot 应用
./gradlew bootRun

# 构建可执行的 Spring Boot JAR
./gradlew bootJar

# 显示 Spring Boot 相关任务
./gradlew tasks --group spring-boot
```

## 代码质量检查

```bash
# 运行 Checkstyle 检查
./gradlew checkstyleMain
./gradlew checkstyleTest

# 运行 PMD 静态分析
./gradlew pmdMain
./gradlew pmdTest

# 运行 SpotBugs 检查
./gradlew spotbugsMain
./gradlew spotbugsTest

# 运行所有代码质量检查
./gradlew check
```

## 测试和覆盖率

```bash
# 运行测试并生成覆盖率报告
./gradlew jacocoTestReport

# 运行特定测试
./gradlew test --tests com.example.MyTest
./gradlew test --tests "*IntegrationTest"

# 跳过测试进行构建
./gradlew build -x test

# 运行测试并生成 HTML 报告
./gradlew test jacocoTestReport
```

## 发布和部署

```bash
# 发布到本地 Maven 仓库
./gradlew publishToMavenLocal

# 发布到远程仓库（需要配置）
./gradlew publish

# 生成 POM 文件
./gradlew generatePomFileForMavenJavaPublication
```

## 依赖管理

```bash
# 更新依赖
./gradlew dependencies --refresh-dependencies

# 检查过时的依赖
./gradlew dependencyUpdates

# 分析依赖关系
./gradlew dependencyInsight --dependency slf4j-api
./gradlew dependencyInsight --configuration compileClasspath --dependency guava
```

## 调试和分析

```bash
# 显示详细的构建信息
./gradlew build --info

# 显示调试信息
./gradlew build --debug

# 显示性能统计
./gradlew build --profile

# 并行构建（多项目）
./gradlew build --parallel

# 配置缓存（实验性功能）
./gradlew build --configuration-cache
```

## Docker 相关（如果有 Docker 插件）

```bash
# 构建 Docker 镜像
./gradlew dockerBuildImage

# 推送 Docker 镜像
./gradlew dockerPushImage

# 运行 Docker 容器
./gradlew dockerRun
```

## Flink 相关命令（根据你的项目）

```bash
# 提交 Flink 作业（如果有相应插件）
./gradlew flinkRun

# 生成 Flink SQL 客户端脚本
./gradlew generateSqlClientScripts
```

## 常用组合命令

```bash
# 完整的 CI/CD 流程
./gradlew clean build test jacocoTestReport

# 快速构建（跳过测试和文档）
./gradlew assemble -x test -x javadoc

# 开发模式构建
./gradlew build --continuous

# 生成所有报告和文档
./gradlew build javadoc sourcesJar jacocoTestReport dependencyUpdates
```

## 版本管理

```bash
# 查看 Gradle 版本
./gradlew --version

# 升级 Gradle Wrapper
./gradlew wrapper --gradle-version 8.5

# 生成 wrapper（如果没有）
./gradlew wrapper
```

## 实用技巧

### 1. 指定 JVM 参数

```bash
./gradlew build -Dorg.gradle.jvmargs="-Xmx2g -XX:MaxMetaspaceSize=512m"
```

### 2. 离线模式构建

```bash
./gradlew build --offline
```

### 3. 构建扫描（在线分析）

```bash
./gradlew build --scan
```

### 4. 指定构建文件

```bash
./gradlew build -b custom-build.gradle
```

### 5. 指定项目目录

```bash
./gradlew build -p ../other-project
```

## 针对你的 Flink 项目的常用命令

基于你的 `build.gradle`，以下是一些特别有用的命令：

```bash
# 清理并构建
./gradlew clean build

# 运行应用程序
./gradlew run

# 查看依赖树
./gradlew dependencies

# 运行测试
./gradlew test

# 生成可执行 JAR
./gradlew build

# 检查配置问题
./gradlew build --warning-mode=all

# 查看所有可用任务
./gradlew tasks
```

## 命令行选项总结

| 选项                     | 说明                   |
| ------------------------ | ---------------------- |
| `--help`, `-h`           | 显示帮助               |
| `--version`, `-v`        | 显示版本               |
| `--quiet`, `-q`          | 安静模式               |
| `--info`, `-i`           | 显示详细信息           |
| `--debug`, `-d`          | 调试模式               |
| `--stacktrace`, `-s`     | 显示堆栈跟踪           |
| `--scan`                 | 生成构建扫描           |
| `--no-scan`              | 禁用构建扫描           |
| `--profile`              | 生成性能报告           |
| `--continue`             | 继续构建即使有任务失败 |
| `--parallel`             | 并行执行项目           |
| `--max-workers`          | 设置最大工作线程数     |
| `--offline`              | 离线模式               |
| `--refresh-dependencies` | 刷新依赖               |
| `--configure-on-demand`  | 按需配置               |
| `--build-file`           | 指定构建文件           |
| `--project-dir`          | 指定项目目录           |
| ------------------------ | ---------------------- |
