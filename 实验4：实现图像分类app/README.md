# 使用TensorFLow Lite模型制作器和Android Studio ML模型绑定来识别花朵


## 介绍

这个测试版代码实验室介绍了使用TensorFlow Lite ModelMaker和Androidstudio4.1Beta 1或更高版本的最新工具。此外，它将需要访问物理Android设备进行测试。如果您更喜欢使用这个代码实验室的稳定版本，请使用这个代码实验室。



## 向应用中添加TensorFlow Lite

![图 1](images/957be474ea826120d16c841cbd465619449d1e29d7096d354dec3b3d88ea4b7f.png)  


## 检查代码中的TODO项

本项目初始代码中包括了若干的TODO项，以导航项目中未完成之处。为了方便起见，首先查看TODO列表视图，View>Tool Windows>TODO

![图 2](images/e2dea654e7448fbc1b504ed50e131abde4bf56cdd0748eb5a73bde9a3596ec4b.png)  

默认情况下了列出项目所有的TODO项，进一步按照模块分组（Group By）

![图 3](images/0d04a29025f367fdb0e5f5634b967fbb6f9b5754bca317c2e389eab33426fc51.png)  



## 添加代码重新运行APP

1.定位“start”模块MainActivity.kt文件的TODO 1，添加初始化训练模型的代码
![图 4](images/e50a9d5147b8fbc2be904f75d54ea8cde653436293d688d589c2826ef1d6a941.png)  

2.在CameraX的analyze方法内部，需要将摄像头的输入ImageProxy转化为Bitmap对象，并进一步转化为TensorImage 对象
![图 5](images/0ce6064603ba19e4e9128525112b2d65f576c7764c918bf9fb3388815801bd95.png)  

3.对图像进行处理并生成结果，主要包含下述操作：

按照属性score对识别结果按照概率从高到低排序列出最高k种可能的结果，k的结果由常量MAX_RESULT_DISPLAY定义

![图 6](images/0d4367e7e8f2c45249d7553ceea175d091913ac2a7960ae2327db51a73891e9b.png)  

4.将识别的结果加入数据对象Recognition 中，包含label和score两个元素。后续将用于RecyclerView的数据显示
![图 7](images/870915fc7a6aeb173ffae927a318d2e650319c70cdcd1d99301b58013e2b2286.png)  

5.将原先用于虚拟显示识别结果的代码注释掉或者删除

![图 8](images/eac4a1838702157ffe76a5c6f10e82a51d9bc9606b07c1406c260694caa135a4.png)  

6.以物理设备重新运行start模块

7.最终运行效果

![图 9](images/18bde5f81279f30ce819bd061d36f192b458eebcd5fdf7cd29ab35442ef4c0dc.png)  

![图 10](images/aee374d0994685fcfe6277c212b4bff68b4f474708c6e9145db8bfd2fadce1ee.png)  

![图 11](images/30ef5973d5fda386d2639673c686a112df0a76a2edfe83bba8c783b09799f3aa.png)  

![图 12](images/6b5e34c2cc6d1e789b582dea5dee5b79fbcac9086117541ea261f32487afc89d.png)  

![图 13](images/b15a693fe5d11c28d7faa5044ce28011f8b9245053a59d53f04ab058f7a87620.png)  
