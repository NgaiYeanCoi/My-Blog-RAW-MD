---
title: AI与区块链选修第九章测验图解
top: false
cover: false
toc: true
mathjax: true
date: 2024-04-15 20:30:02
tags:
password:
summary:
categories:
- [university]
math:
---

## 前言

- 在学习通上老师给的解析还不够详细仍然缺少了些细节

- 这里将一步步拆解老师给的解析
- 大家可以来使用我整理的数据集对于完成作业已经足够了    

## 步骤

- 打开[百度智能云网站](https://ai.baidu.com/easydl/)
点击【立即使用】在【在线使用】【图像:文心大模型】这一弹出【选择模型类型】，列选择【物体检测】

![图片1](../image/ai/1Weixin%20Screenshot_20240415204756.png)

![图片2](../image/ai/2Weixin%20Screenshot_20240415205106.png)

<!--more-->

- 有账号就直接登录无账号就注册

![图片3](../image/ai/3.3.png)

-点击训练模型
![图片3](../image/ai/3Weixin%20Screenshot_20240415205826.png)

-填入个人信息其他复制粘贴就好

模型名称:输入【垃圾识别】
所属行业:【其他】
行业描述:垃圾分类
应用场景：【为批量图片自动打标签应用场景】
业务描述:【为了解决垃圾分类问题】
![图片4](../image/ai/4Weixin%20Screenshot_20240415210106.png)
- 出现这个对话框不用理会直接点确定
![图片4](../image/ai/Weixin%20Screenshot_20240415210148.png)

- 这里勾选半监督按钮
![图片4](../image/ai/5Weixin%20Screenshot_20240415211008.png)

- 点击创建数据集
  ![图片](../image/ai/6Weixin%20Screenshot_20240415211407.png)
- 填入名称
![图片](../image/ai/8Weixin%20Screenshot_20240415211521.png)
- 点击创建并导入
![图片](../image/ai/7Weixin%20Screenshot_20240415211621.png)

- 配置成图片一样的
![图片](../image/ai/9Weixin%20Screenshot_20240415211738.png)
可以上传我提供的素材
[下载](https://gitee.com/NYC1/temp/blob/master/%E7%AD%9B%E9%80%89.zip)

上传好了就确认
![图片](../image/ai/10Weixin%20Screenshot_20240415212604.png)

静静等待他导入好
![图片](../image/ai/11Weixin%20Screenshot_20240415212708.png)
- 导入好之后点击左边的在线标注
![图片](../image/ai/12Weixin%20Screenshot_20240415213018.png)
点击标注
![图片](../image/ai/13Weixin%20Screenshot_20240415213107.png)
点击添加标签逐次添加学习通要求的 餐巾纸、快餐盒、易拉罐、空的塑料袋以及满的垃圾袋进标签
![图片](../image/ai/14Weixin%20Screenshot_20240415213216.png)
点击左上的的图标画一个矩形把包含的物体到方框内然后选择对于的标签
![图片](../image/ai/15Weixin%20Screenshot_20240415213620.png)
每个都这样一个一个添加完之后

- 点击左侧的模型训练

![图片](../image/ai/15Weixin%20Screenshot_20240415213826.png)
选择已有模型
![图片](../image/ai/16Weixin%20Screenshot_20240415213907.png)
出现这个不用理会
![图片](../image/ai/17Weixin%20Screenshot_20240415213944.png)
注意：为了方便演示这里的标签是不完整的标签全选就好
按照图片配置如下：
![图片](../image/ai/18Weixin%20Screenshot_20240415214347.png)
- 训练环境按照照片配置
![图片](../image/ai/19Weixin%20Screenshot_20240415214444.png)
然后开始训练就好


- 静静等待他训练好大约要1.5个小时

![图片](../image/ai/20Screenshot_20240415214544.png)

- 训练完之后大概是这样的
![图片](../image/ai/21Weixin%20Screenshot_20240415214706.png)

## 检验
上传一张带你所训练的模型的图片来检验一下准确性
![图片](../image/ai/21Weixin%20Screenshot_20240415222208.png)

保存下面的图片去试试
![图片](../image/ai/images.jpg)