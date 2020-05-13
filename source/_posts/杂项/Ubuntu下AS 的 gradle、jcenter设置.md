---
date: 2020-01-22 11:34:18
tags:
    - 杂项
---

# gradle
下载AS sync时显示的gradle版本
下载地址：[http://services.gradle.org/distributions/](http://services.gradle.org/distributions/)

将下载好的zip 文件放在~/.gradle/wrapper/dists/gradle-5.6.4-all/ankdp27end7byghfw1q2sw75f/   下，不用解压缩。（不同版本的gradle对应的目录不一样）
这样AS sync的时候就不会卡在下载gradle的时候了。

# jcenter

修改项目根目录下面的build.gradle文件，将jcenter()库注释掉，添加阿里的maven库，同时保留Google的maven库地址即可。
```
// Top-level build file where you can add configuration options common to all sub-projects/modules.
buildscript {
    repositories {
        google()
        //jcenter()
        maven{url 'http://maven.aliyun.com/nexus/content/groups/public/'}
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:3.5.1'
        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}

allprojects {
    repositories {
        google()
        //jcenter()
        maven{url 'http://maven.aliyun.com/nexus/content/groups/public/'}
    }
}

task clean(type: Delete) {
    delete rootProject.buildDir
}
```

