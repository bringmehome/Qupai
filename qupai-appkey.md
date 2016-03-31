##Description: qupai

* [initQuPai](#1)

* [startQuPai](#2)

* [返回码](#3)

##**概述**


#**initQuPai**<div id="1"></div>

    初始化趣拍

    initQuPai({params}, callback(ret, err))

##params

appkey：

- 类型：字符串
- 默认值：无
- 描述：申请的appKey

appsecret：

- 类型：字符串
- 默认值：无
- 描述：申请的appsecret

space：

- 类型：字符串
- 默认值：无
- 描述：视频存储目录 建议使用uid cid之类的信息

##callback(ret,err)

ret：

- 类型：JSON对象

内部字段：

```js
{
    code : 0              //返回码
    message:"success"     //正确返回
}
```

err：

- 类型：JSON对象

内部字段：

```js
{
    code : 702            //错误码
    message:  ""          //错误描述
}
```

##示例代码

```js
var qupai = api.require('qupai');
var params = {
    appKey:'2049xxxxxxa7c36',
    appsecret:'55e40xxxxxxxxxxxxa29xxxxb58',
    space:'uid'
}
qupai.initQuPai(params, function(ret, err){
    if(ret)
        alert(JSON.stringify(ret));
    else
        alert("err = "+JSON.stringify(err));
});
```

##补充说明

    无

##可用性

    Android系统, iOS系统

    可提供的1.0.0及更高版本


#**startQuPai**<div id="2"></div>

    打开拍摄视频的页面

    startQuPai({params},function(ret, err))

##params

maxDuration：
- 类型：number
- 默认值：8
- 描述：允许拍摄的最大时长，时长越大，产生的视频文件越大；

minDuration：
- 类型：number
- 默认值：2
- 描述：允许拍摄的最短时长；

videoBitrate：
- 类型：number
- 默认值：800 * 1024
- 描述：视频码率，建议8001000-50001000,码率越大，视频越清析，视频文件也会越大。参考：8秒的视频以2000*1000的码率压缩，文件大小1.5M-2M。

videoWidth：
- 类型：number
- 默认值：480
- 描述：输出视频的尺寸>宽；//输出视频的尺寸–建议320*240 480*480 360*640

videoHeight：
- 类型：number
- 默认值：480
- 描述：输出视频的尺寸>高；//输出视频的尺寸–建议320*240 480*480 360*640

captureHeight：
- 类型：number
- 默认值：118
- 描述：拍摄布局高度；

beautySkinOn：
- 类型：布尔型
- 默认值：false
- 描述：美颜是否显示

beautyProgress：
- 类型：number
- 默认值：80
- 描述：美颜参数；

flashLightOn：
- 类型：布尔型
- 默认值：false
- 描述：闪光灯是否显示

timelineIndicator：
- 类型：布尔型
- 默认值：false
- 描述：时间提示是否显示

cameraFacing：
- 类型：number
- 默认值：0
- 描述：1 开启前摄像头, 0 开启后摄像头

##callback(ret,err)

ret：

- 类型：JSON对象
- 描述：返回的文件路径，和视频长度

内部字段：

```js
{
    code : 0              //返回码
    data:{
        videoPath: "/storage/emulated/0/Sins/sin_2016-03-27-23-07-20-039.mp4",   //视频文件路径
        imgPath: "/storage/emulated/0/Sins/sin_2016-03-27-23-07-20-039.png",     //图片文件路径
        duration: 2903                                                           //视频时长(单位:ms)
    }
}
```

err：

- 类型：JSON对象

内部字段：

```js
{
    code : 9002                //返回码
    message:"Canceled."        //错误描述
}
```

##示例代码

```js
var qupai = api.require('qupai');

var params = {
    maxDuration：8,
    minDuration：2,
    videoBitrate：1024*1000,
    videoWidth：360,
    videoHeight：640,
    captureHeight：118,
    beautySkinOn：true,
    beautyProgress：80,
    flashLightOn：true,
    timelineIndicator：true,
    cameraFacing：1
};

qupai.startQuPai(params,function(ret, err){
    if(ret)
        alert(JSON.stringify(ret));
    else
        alert("err = "+JSON.stringify(err));
});
```

##可用性

    Android系统, iOS系统

    可提供的1.0.0及更高版本


#**upload**<div id="3"></div>

    上传视频

    upload({params}, callback(ret, err))

##params

videoPath：
- 类型：字符串
- 描述：录制视频的路径

imgPath：
- 类型：字符串
- 描述：缩略图路径；

shareType：
- 类型：number
- 默认值：1
- 描述：是否公开 0公开分享 1私有(default) 公开类视频不需要AccessToken授权；

description：
- 类型：字符串类型
- 描述：描述信息；

tags：
- 类型：字符串类型
- 描述：标签 多个标签用 "," 分隔符

##callback(ret,err)

ret：

- 类型：JSON对象
- 描述：返回的文件路径，和视频长度

内部字段：

```js
{
    code : 0,            //返回码
    remoteId: "",        //字符串类型；上传成功中返回视频在服务端存储的remoteId
    progress: 0.2        //字符串类型；上传进度 (上传未完成时候ret只有这个属性传输上传进度值)
}
```

err：

- 类型：JSON对象

内部字段：

```js
{
    code : 9002                //返回码
    message:"Canceled."        //错误描述
}
```

##示例代码

```js
var qupai = api.require('qupai');

var params = {
    videoPath:"",
    imgPath:"",
    shareType:1,
    description:"测试视频",
    tags:"视频,录制"
};

qupai.startQuPai(params,function(ret, err){
    if(ret)
        alert(JSON.stringify(ret));
    else
        alert("err = "+JSON.stringify(err));
});
```

##可用性

    Android系统, iOS系统

    可提供的1.0.0及更高版本


#**返回码**<div id="4"></div>

0        正确返回

1        请求参数错误

2        初始化失败

9002     Canceled

9003     Upload failure.