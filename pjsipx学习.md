
# PJSIP源码编译Android so库

## 编译环境：ubantu 16.04 + JDK 1.8 + NDK 15

## 步骤

### 1 [下载pjsip源码](http://www.pjsip.org/),下载时请下载tar.bz2 压缩包

### 2 在pjlib/include/pj 目录下创建config_site.h文件，文件中添加以下内容
    /* Activate Android specific settings in the 'config_site_sample.h' */
    #define PJ_CONFIG_ANDROID 1
    #include <pj/config_site_sample.h>
 
### 3 需提前配置jdk、sdk环境变量，进入pjsip主目录，执行以下指令，编译.o文件
	 ./configure-android 
     make dep && make clean && make
### 4 执行成功之后，进入到swig目录，执行make指令，编译生成so以及cpp文件
    cd pjsip-apps/src/swig/
    make clean 
    make 
### 5 pjsip-apps/src/swig/java/android/ 目录下即为编译创建好的android示例，pjsip-apps/src/swig/java/output


备注:环境变量配置参考

     export  ANDROID_ABI="armeabi-v7a"
     export  ANDROID_NDK=/usr/android/android-ndk-r15c
     export  ANDROID_SDK=/home/test/android-sdk-linux

     export ANDROID_NDK_ROOT=$ANDROID_NDK
     export ANDROID_NDK_HOME=$ANDROID_NDK
     export ANDROID_HOME=$ANDROID_SDK
     export PATH=$ANDROID_SDK/platform-tools:${PATH}

     export JAVA_HOME=/usr/java/jdk1.8.0_181
     export JRE_HOME=${JAVA_HOME}/jre
     export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
     export PATH=${JAVA_HOME}/bin:$PATH

	 //下载sdk,并配置环境变量
     curl --location http://dl.google.com/android/android-sdk_r22.3-linux.tgz | tar -x -z -C $HOME
     export ANDROID_HOME=$HOME/android-sdk-linux
     export PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools
     ( sleep 5 && while [ 1 ]; do sleep 1; echo y; done ) | android update sdk --no-ui --filter platform-tool,android-19,sysimg-19,build-tools-19.0.1

		
	 //下载安装ssh插件 安装成功之后可以使用第三方工具连接
     sshd
     The program 'sshd' is currently not installed. You can install it by typing:
     apt install openssh-server


