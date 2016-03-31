##Description: qupai

* [initQuPai](#1)

* [startRecord](#2)

* [upload](#3)

* [返回码](#4)

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

domain：

- 类型：字符串
- 默认值：无
- 描述：自己在微视频云服务上创建的空间访问域名：如：http://sin.s.qupai.me

##callback(ret,err)

ret：

- 类型：JSON对象

内部字段：

```js
{
    code : 200              //返回码
    token:"xxx..."          //token
}
```

err：

- 类型：JSON对象

内部字段：

```js
{
    code : 201                              //错误码
    message:  "Parameter is null."          //错误描述
}
```

##示例代码

```js
var qupai = api.require('qupai');
var param = {
        appkey:"2065cf0d3f027af",
        appsecret:"5db5a1b18c214004a7003a0c61cbecf3",
        space:"20160331",
        domain:"http://sin.s.qupai.me"
    };
qupai.initQuPai(param, function(ret, err){
    if(ret)
        alert(JSON.stringify(ret));
    else
        alert(JSON.stringify(err));
});
```

##补充说明

    无

##可用性

    Android系统, iOS系统

    可提供的1.0.0及更高版本


#**startRecord**<div id="2"></div>

    打开拍摄视频的页面

    startRecord({params},function(ret, err))

##params

maxDuration：
- 类型：number
- 默认值：8
- 描述：允许拍摄的最大时长，时长越大，产生的视频文件越大

minDuration：
- 类型：number
- 默认值：2
- 描述：允许拍摄的最小时长

videoBitrate：
- 类型：number
- 默认值：800 * 1024
- 描述：视频码率，建议600*1000-2000*1000,码率越大，视频越清析，视频文件也会越大。
参考：8秒的视频以2000*1000的码率压缩，文件大小1.5M-2M。请开发者根据自己的业务场景设置时长和码率。

videoWidth：
- 类型：number
- 默认值：480
- 描述：设置输出视频分辨率 宽；//输出视频的尺寸–建议320*240 480*480 360*640

videoHeight：
- 类型：number
- 默认值：480
- 描述：设置输出视频分辨率 高；//输出视频的尺寸–建议320*240 480*480 360*640

captureHeight：
- 类型：number
- 默认值：120
- 描述：拍摄布局高度；

beautySkinOn：
- 类型：布尔型
- 默认值：false
- 描述：是否开启美颜

beautyDegree：
- 类型：number
- 默认值：80
- 描述：美颜度,百分比，可设置的值为0-100

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
- 描述：设置默认为前置摄像头或后置摄像头,1 开启前摄像头, 0 开启后摄像头

##callback(ret,err)

ret：

- 类型：JSON对象
- 描述：返回的文件路径，和视频长度

内部字段：

```js
{
    code : 200                                                                   //返回码
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
    code : 2003                //返回码
    message:""                 //错误描述
}
```

##示例代码

```js
var qupai = api.require('qupai');

var params = {
    maxDuration:10,
    minDuration:5,
    videoBitrate:1024*1000,
    videoWidth:360,
    videoHeight:640,
    captureHeight:118,
    beautySkinOn:true,
    beautyDegree:80,
    flashLightOn:true,
    timelineIndicator:true,
    cameraFacing:1
};
qupai.startRecord(params, function(ret, err){
    if(ret){
        alert(JSON.stringify(ret));
    }else
        alert(JSON.stringify(err));
});
```

##可用性

    Android系统, iOS系统

    可提供的1.0.0及更高版本


#**upload**<div id="3"></div>

    上传视频

    upload({params}, callback(ret, err))

##params

videoUrl：
- 类型：字符串
- 描述：远程视频地址

imgUrl：
- 类型：字符串
- 描述：远程缩略图地址

progress：
- 类型：number
- 描述：文件上传进度(百分比)

##callback(ret,err)

ret：

- 类型：JSON对象
- 描述：返回的文件路径，和视频长度

内部字段：

```js
{
    code : 203,             //返回码
    progress: 75           //字符串类型；上传进度 (上传未完成时候ret只有这个属性传输上传进度值)
}

或者

{
    code : 200,                                            //返回码
    data: {
        videoUrl: "http://sin.s.qupai.me/v/d....mp4...",   //视频文件路径
        imgUrl: "http://sin.s.qupai.me/v/d...jpg...",      //图片文件路径
    }
}
```

err：

- 类型：JSON对象

内部字段：

```js
{
    code :            //返回码
    message:""        //错误描述
}
```

##示例代码

```js
var qupai = api.require('qupai');

var param = {
        videoPath:vpath,
        imgPath:ipath
};

qupai.upload(param, function(ret, err){
    if(ret)
        alert(JSON.stringify(ret));
    else
        alert(JSON.stringify(err));
});
```

##可用性

    Android系统, iOS系统

    可提供的1.0.0及更高版本


#**返回码**<div id="4"></div>

200        Success

201        Parameter is null.

203        文件正在上传.

1101 Host（请求的域名） 未授权， 通常都是域名地址错误导致

1102 appSecret不正确

1103 bundleId不正确

1104 包名和签名为空

1105 包名或签名不正确

1106 存储空间里的目录不正确

1107 AppKey不正确