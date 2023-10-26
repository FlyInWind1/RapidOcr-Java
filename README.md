# RapidOcr-Java

## 🪧 项目起源

- 现有的JavaOCR工具包识别效果差强人意，PaddleOCR在实现前沿算法的基础上，考虑精度与速度的平衡，进行模型瘦身和深度优化，使其尽可能满足产业落地需求。

- PaddleOCR官方并未提供Java版本，而[RapidOcr](https://github.com/RapidAI/RapidOCR)解决了这个问题，其提供了Kotlin和Java混合版本的[Demo-onnx](https://github.com/RapidAI/RapidOcrOnnxJvm)和[Demo-ncnn](https://github.com/RapidAI/RapidOcrNcnnJvm)

  >RapidOcr是完全开源、免费并支持多平台、多语言OCR离线部署

- 而实际使用过程中，项目中并不想再引入Kotlin，因此本项目将Kotlin部分移除，并在此基础上加以完善(提供了更友好的的调用方法)，更方便java开发者使用。

## 👏 项目特点

- 纯Java代码调用RapidOcr
- 使用ncnn和onnx推理引擎方式，并编写了简单工具类，默认使用Onnx推理方式
- 均使用CPU版本，GPU版本请自行编译

> ⚠️ 注意：当前JVM启动时**只能同时启动一种推理引擎**


## 🎉 快速开始

1⃣️ 引入jar包(需要自己下载项目打包，过程参考[如何自行编译jar包？](./docs/COMPILE_JAR.md))

```xml
<dependency>
    <groupId>com.github.monster</groupId>
    <artifactId>RapidOcr-Java</artifactId>
    <version>latest.version</version>
</dependency>
```

2⃣️ 调用(更多使用示例请参考[测试类](https://github.com/MyMonsterCat/RapidOcr-Java/blob/main/src/test/java/com/github/monster/ocr/OcrUtilTest.java))

```java
public class OcrUtilTest {

    @Test
    public void NcnnTest() {
        // 使用NCNN引擎进行识别，不要同ONNX使用
        OcrResult NCNNResult = OcrUtil.runOcr(getResourcePath("/images/40.png"), LibConfig.getNcnnConfig(), ParamConfig.getDefaultConfig(), HardwareConfig.getNcnnConfig());
        Assert.assertEquals("40", NCNNResult.getStrRes().trim().toString());
    }

    @Test
    public void OnnxTest() {
        String imgPath = getResourcePath("/images/40.png");
        // 使用ONNX推理引擎进行识别，不要同NCNN使用
        OcrResult ONNXResult = OcrUtil.runOcr(imgPath);
        Assert.assertEquals("40", ONNXResult.getStrRes().trim().toString());
    }
}
```

## 🔝 进阶使用

- [参数调优、版本说明、目录说明、分支说明](./docs/ADVANCED.md)
- [如何自行更新模型？](./docs/UPDATE_MODEL.md)
- [如何自行编译动态库？](./docs/COMPILE_LIB.md)
- [如何自行编译jar包？](./docs/COMPILE_JAR.md)
- OCR相关知识-待更新
- JVM下不同PaddleOCR调用方式性能比对-待更新

## 📌 TODO

- [x] 根据系统版本自适应加载动态库
- [x] 动态库集成到jar中
- [x] 是否删除临时文件夹配置为可选项
- [x] jvm未退出场景连续调用识别结果集乱码[#1](https://github.com/MyMonsterCat/RapidOcr-Java/issues/1)
- [x] 集成ONNX[#2](https://github.com/MyMonsterCat/RapidOcr-Java/issues/2)，感谢[nn200433](https://github.com/nn200433)及[tika-server](https://github.com/nn200433/tika-server)👏 
- [x] 添加日志，规范日志打印
- [x] ONNX支持Mac-Arm64

## 鸣谢

- [RapidOCR](https://github.com/RapidAI/RapidOCR)
- [PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR)

## 开源许可

使用 [Apache License 2.0](https://github.com/MyMonsterCat/DeviceTouch/blob/main/LICENSE)
