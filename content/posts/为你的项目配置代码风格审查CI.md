---
title: "为你的项目配置代码风格审查CheckStyle与CI测试"
date: 2020-08-03T22:02:15+08:00
draft: false
---

## why？

多人协作项目中，每个人的代码风格习惯可能不一样，而且有一些写法容易造成歧义，
比如`if`后不加花括号。

使用代码风格审查工具可以帮助我们强制要求代码的写法。

## 使用Maven CheckStyle插件

[Maven CheckStyle plugin](https://maven.apache.org/plugins/maven-checkstyle-plugin/)

[审查规则xml 配置例子](https://checkstyle.sourceforge.io/sun_style.html)

### POM.xml 中配置插件

```
<plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-checkstyle-plugin</artifactId>
                <version>3.1.1</version>
                <configuration>
                    <configLocation>${basedir}/.circleci/checkstyle.xml</configLocation>
                    <includeTestSourceDirectory>true</includeTestSourceDirectory>
                    <enableRulesSummary>false</enableRulesSummary>
                </configuration>
                <executions>
                    <execution>
                        <id>verify</id>
                        <phase>verify</phase>
                        <goals>
                            <goal>check</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
```

`configLocation`配置文件路径，可以参考上面的例子。

`<executions` 绑定plugin执行的Maven默认生命周期的阶段，这里是`verify`

## 使用[CircleCI](https://s0circleci0com.icopy.site/docs/2.0/about-circleci/)

Circle是一个免费的CI工具。

Maven的代码审查插件，只是与Maven的生命周期进行绑定，我们还需要保证，在项目组成员提交代码（PR）时，对代码风格进行审查（也就是运行 CheckStyle plugin），通过检查才能合并。

### 在CircleCI上进行配置

登录CircleCI后，可以与Github上的项目进行关联，对我们将要测试的项目生成测试脚本，
会有一个yml配置文件，配置到我们的项目中，类似这样：
```
version: 2
jobs:
  test:
    docker:
      - image: circleci/openjdk:8u212-jdk-stretch
    steps:
      - checkout
      - restore_cache:
          key: haomega-{{ checksum "pom.xml" }}
      - run:
          name: Run Maven verify
          command: mvn clean verify
      - save_cache: # saves the project dependencies
          paths:
            - ~/.m2
          key: haomega-{{ checksum "pom.xml" }}
workflows:
  version: 2
  default:
    jobs:
      - test

```

当有PR时，会自动运行测试脚本。