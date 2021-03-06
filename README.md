# Paddle-Lite-Demo


## 功能
* iOS示例: 
    * 静态图像目标分类和视频流目标分类；
    * 静态图像目标检测、相机拍照目标检测、相机视频流目标检测;
* Android示例: 
    * 基于MobileNetV1的图像分类；
    * 基于MobileNetV1-SSD的目标检测；

## 要求

* iOS
    * Mac机器，需要有xcode环境（已验证：Xcode Version 10.1 (10B61)
    * 对于ios 12.x版本，如果提示“xxx.  which may not be supported by this version of Xcode”，请下载对应的[工具包]( https://github.com/iGhibli/iOS-DeviceSupport), 下载完成后解压放到/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/DeviceSupport目录，重启xcode

* Android
    * Android Studio 3.4
    * Android手机或开发版，NPU功能暂时只在麒麟810和990芯片的华为手机（如Nova5系列）进行了测试，使用前请将EMUI更新到最新版本；

## 安装
$ git clone https://github.com/PaddlePaddle/Paddle-Lite-Demo

* iOS
    * 下载opencv framework, 下载完成后解压到`ios-xxx_demo/xxx_demo/`目录下
    ```bash
    wget https://paddle-inference-dist.bj.bcebos.com/PaddleLiteDemo/opencv2.framework.zip
    ```
    * 打开xcode，点击“Open another project…”打开`Paddle-Lite-Demo/ios-xxx_demo/`目录下的xcode工程；
    * 在选中左上角“project navigator”，选择“classification_demo”，修改“General”信息；
    * 插入ios真机（已验证：iphone8， iphonexr），选择Device为插入的真机；
    * 点击左上角“build and run”按钮；

* Android
    * 打开Android Studio，在"Welcome to Android Studio"窗口点击"Open an existing Android Studio project"，在弹出的路径选择窗口中进入"PaddleLite-android-demo"目录，然后点击右下角的"Open"按钮即可导入工程
    * 通过USB连接Android手机或开发板；
    * 载入工程后，点击菜单栏的Run->Run 'App'按钮，在弹出的"Select Deployment Target"窗口选择已经连接的Android设备，然后点击"OK"按钮；
    * 手机上会出现Demo的主界面，选择第一个"Image Classification"图标，进入基于MobileNetV1的图像分类示例程序；
    * 在图像分类Demo中，默认会载入一张猫的图像，并会在图像下方给出CPU的预测结果，如果你使用的是麒麟810或990芯片的华为手机（如Nova5系列），可以在右上角的上下文菜单选择"Settings..."打开设置窗口切换NPU模型进行预测；
    * 在图像分类Demo中，你还可以通过上方的"Gallery"和"Take Photo"按钮从相册或相机中加载测试图像；

## 更新到最新的预测库
* Paddle-Lite项目：https://github.com/PaddlePaddle/Paddle-Lite
* 参考 [Paddle-Lite文档](https://github.com/PaddlePaddle/Paddle-Lite/wiki)，编译IOS预测库或者Android预测库
* 编译最终产物位于 `build.lite.xxx.xxx.xxx` 下的 `inference_lite_lib.xxx.xxx`
### IOS更新预测库
* 替换库文件：产出的`lib`目录替换`ios-classification_demo/classification_demo/lib`目录
* 替换头文件：产出的`include`目录下的文件替换`ios-classification_demo/classification_demo/paddle_lite`目录下的文件

### Android更新预测库
* 仅支持CPU
  * 替换jar文件：将PaddleLite编译生成的build.lite.android.xxx.gcc/inference_lite_lib.android.xxx/java/jar/PaddlePredictor.jar替换demo中的PaddleLite-android-demo/app/libs/PaddlePredictor.jar
  * 替换arm64-v8a jni库文件：将Paddle-Lite编译生成build.lite.android.armv8.gcc/inference_lite_lib.android.armv8/java/so/libpaddle_lite_jni.so库替换demo中的PaddleLite-android-demo/app/src/main/jniLibs/arm64-v8a/libpaddle_lite_jni.so
  * 替换armeabi-v7a jni库文件：将Paddle-Lite编译生成的build.lite.android.armv7.gcc/inference_lite_lib.android.armv7/java/so/libpaddle_lite_jni.so库替换demo中的PaddleLite-android-demo/app/src/main/jniLibs/armeabi-v7a/libpaddle_lite_jni.so.

* 支持CPU和NPU
  * 替换jar文件：将PaddleLite编译生成的build.lite.npu.android.xxx.gcc.cxx_shared.tiny_publish/inference_lite_lib.android.xxx.npu/java/jar/PaddlePredictor.jar替换demo中的PaddleLite-android-demo/app/libs/PaddlePredictor.jar
  * 替换arm64-v8a jni库文件：将Paddle-Lite编译生成build.lite.npu.android.armv8.gcc.cxx_shared.tiny_publish/inference_lite_lib.android.armv8.npu/java/so/libpaddle_lite_jni.so库替换demo中的PaddleLite-android-demo/app/src/main/jniLibs/arm64-v8a/libpaddle_lite_jni.so
  * 替换armeabi-v7a jni库文件：将Paddle-Lite编译生成的build.lite.npu.android.armv7.gcc.cxx_shared.tiny_publish/inference_lite_lib.android.armv7.npu/java/so/libpaddle_lite_jni.so库替换demo中的PaddleLite-android-demo/app/src/main/jniLibs/armeabi-v7a/libpaddle_lite_jni.so.

  编译支持NPU的jni库，需要在Paddle-Lite源码下使用$ ./lite/tools/build_npu.sh --arm_abi=armv8 tiny_publish命令编译生成armv64-v8a的libpaddle_lite_jni.so，armeabi-v7a的libpaddle_lite_jni.so请将编译命令中的--arm_abi=armv8改为--arm_abi=armv7，但由于华为最新的DDK库并没有发布，可能无法完成相关编译工作，因此，如果想使用NPU功能，强烈建议使用demo中自带的libpaddle_lite_jni.so和HIAI DDK库；

## 效果展示

* iOS
    * mobilenetv1 目标分类

    ![ios_static](doc/ios_static.jpg)      ![ios_video](doc/ios_video.jpg)

    * mobilenetv1-ssd 目标检测
    
    ![ios_static](doc/ios-image-detection.jpg)      ![ios_video](doc/ios-video-detection.jpg)

* Android
    * mobilenetv1 目标分类

      - CPU预测结果（测试环境：华为nova5）

      ![android_image_classification_cat_cpu](doc/android_image_classification_cat_cpu.jpg)      ![android_image_classification_keyboard_cpu](doc/android_image_classification_keyboard_cpu.jpg)

      - NPU预测结果（测试环境：华为nova5）

      ![android_image_classification_cat_npu](doc/android_image_classification_cat_npu.jpg)      ![android_image_classification_keyboard_npu](doc/android_image_classification_keyboard_npu.jpg)
 
    * mobilenetv1-ssd 目标检测

      - CPU预测结果（测试环境：华为nova5）

      ![android_object_detection_dog_npu](doc/android_object_detection_dog_cpu.jpg)

      - NPU预测结果（测试环境：华为nova5）

      待支持
    