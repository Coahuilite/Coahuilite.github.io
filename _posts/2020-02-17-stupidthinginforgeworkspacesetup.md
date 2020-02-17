---
layout: post
title: 设置Forge工作区时发生的蠢事
date: 2020-02-17
Author: Fe
categories: 
tags: [原创,Minecraft，Java]
comments: true
---

## 设置Forge工作区时发生的蠢事

#### 真不敢相信，我居然浪费了这么多时间

翻看自己的“关于”的时候想起自己有个MC的mod坑，然而我喜闻乐见的又给忘了23333...

总之，为了避免返校后可能的网络问题~~以及可能随时会双忘记的风险~~我决定直接先把Forge的工作环境给搞定下来。

##### 关于Forge

Forge是一个用于简化Minecraft mod的加载与兼容性问题而诞生的模组加载器。在forge之前玩家普遍使用ModLoader进行mod载入，更早的时候干脆就是去魔改游戏.jar的方式来载入mod。尽管使用ModLoader比魔改jar的方式来的方便安全，但很显然还是很麻烦，并且制作ML的mod不易，不适合没有带路dalao的萌新，像我这种。

##### Forge工作区的建立

*因使用Windows，故只用Windows进行举例*

首先，既然是要设置Forge工作区，总得有个Forge Mdk，所以迅速前往[forge下载站](http://files.minecraftforge.net/)给自己整了个对应MC版本1.12.2，版本号14.23.5.2846的[Mdk](https://adfoc.us/serve/sitelinks/?id=271228&url=https://files.minecraftforge.net/maven/net/minecraftforge/forge/1.12.2-14.23.5.2846/forge-1.12.2-14.23.5.2846-mdk.zip)...嗷，国内访问这个下载地址可能会因为无法加载广告而根本没法下载，于是简单修改一下下载链接，就可以[下载](https://files.minecraftforge.net/maven/net/minecraftforge/forge/1.12.2-14.23.5.2846/forge-1.12.2-14.23.5.2846-mdk.zip)了。这个版本不是推荐版本，但却是最后版本前的一个最新版本。

下载完成之后解压到想要的目录，可以看到：

```
src
	main
		resources
			pack.mcmeta
			mcmod.info
		java
			com
				example
					examplemod
						ExampleMod.java
gradle
	wrapper
		gradle-wrapper.jar
		gradle-wrapper.properties
eclipse
	.metadata
		.plugins
			org.eclipse.debug.ui
				launchConfigurationHistory.xml
			org.eclipse.debug.core
				.launches
					Server.launch
					Client.launch
			org.eclipse.core.runtime
				.settings
					org.eclipse.ui.prefs
					org.eclipse.ui.ide.prefs
					org.eclipse.ui.editors.prefs
					org.eclipse.jdt.core.prefs
					org.eclipse.epp.usagedata.gathering.prefs
					org.eclipse.debug.ui.prefs
					org.eclipse.core.resources.prefs
			org.eclipse.core.resources
				.root
					0.tree
				.projects
					MDKExample
						.location
README.txt
LICENSE-Paulscode SoundSystem CodecIBXM.txt
LICENSE-Paulscode IBXM Library.txt
LICENSE.txt
gradlew.bat
gradlew
gradle.properties
CREDITS.txt
changelog.txt
build.gradle
.gitignore
```

...这样套娃一般的目录。

不够不需要担心，所有LICENSE开头的txt文件都是许可证内容，跟实际开发无关；CREDITS的内容是致谢信，也跟开发无关；changelog是 ~~变换原木~~ 更变记录，跟开发也没关系；README.txt的内容则重要了许多，但仍然与开发无关但与工作区建立有关，这个之后在说。排除这些无关的内容之后剩下的就是需要用到的东西了，依照[forge文档](https://mcforge-cn.readthedocs.io/)中的内容，build.gradle，gradlew (.bat和.sh)，gradle 文件夹这三个玩意是必不可缺的，这些玩意将会在之后对mod进行构建的过程中发挥作用。

##### 关于Gradle

> Gradle is an open-source build automation tool focused on flexibility and performance. Gradle build scripts are written using a [Groovy](https://groovy-lang.org/) or [Kotlin](https://kotlinlang.org/) DSL. Read about [Gradle features](https://gradle.org/features/) to learn what is possible with Gradle.
>
> - **Highly customizable** — Gradle is modeled in a way that is customizable and extensible in the most fundamental ways.
> - **Fast** — Gradle completes tasks quickly by reusing outputs from previous executions, processing only inputs that changed, and executing tasks in parallel.
> - **Powerful** — Gradle is the official build tool for Android, and comes with support for many popular languages and technologies.
>
> ## [GradleDoc](https://docs.gradle.org/current/userguide/userguide.html#new_projects_with_gradle)

简单点说就是个构建工具，自动的。

嗯，就这样...

熟练使用Win+R打开启动，运行命令提示符，切换到目录，运行`gradlew setupDecompWorkspace`并等待一切搞定....然后遇上了网络问题，很不幸的事情呢。

*猛 男 等 待 中...*

可喜可贺...个鬼，逃过了下载但显然没逃过构建失败，每一次兴奋的等待仅仅等到一行红红的构筑失败，就这样反复的尝试了很多次后决定仔细的审视一下错误信息，于是我发现了“java compiler not found”

嗯？安装的不是JDK吗(警觉)

翻看一下提供的JAVA_HOME路径，我傻了...路径提示我使用的地址是jre的地址，改到jdk的地址后顺利通过了构建...真的是，蠢炸了，居然在这里浪费了如此多的时间。

