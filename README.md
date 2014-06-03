WechatAne
=========

微信ane for ios and android
```
WeixinSdk.instance.register("你的微信appid");
WeixinSdk.instance.addEventListener(StatusEvent.STATUS, onStatus);

function onStatus(e:StatusEvent):void
{ 
	trace(e.code, e.level);
	switch(e.code)
	{
		case "onResp":
			if (e.level == "0")
			{
			//你的分享成功代码
			}
			break;
	}
}

WeixinSdk.instance.sendTextContent(WeixinSdk.WXSceneSession, "text");
WeixinSdk.instance.sendImageContent(WeixinSdk.WXSceneFavorite, bmd);
WeixinSdk.instance.sendAppContent(WeixinSdk.WXSceneTimeline, "title", "content", "http://www.github.com", bmd);
```
如果安卓平台需要回调，请修改android源码，新建一个你的包名.wxapi的包(例如你包名是com.czq.test,需要建一个com.czq.test.wxapi的包)，并且把WXEntryActivity拷过去，否则无法接收回调(发送还是可以的),具体细则看open.weixin.qq.com，需要重新打包Ane。  
再于manifest加入   
```
<activity
	android:name=".wxapi.WXEntryActivity"
	android:label="@string/app_name"
	android:exported="true"
	android:theme="@android:style/Theme.Translucent"
	>
</activity>
```


iOS接收回调的话则是加入
```
<dict>
    <key>CFBundleURLName</key>
    <string>UrlWeixin</string>
    <key>CFBundleURLSchemes</key>
    <array>
      <string>你的微信appid</string>
    </array>
  </dict>
</array>
```

打包ANE请修改build.properties文件，然后在该目录执行ant(必须是osx系统，没有请用虚拟机)