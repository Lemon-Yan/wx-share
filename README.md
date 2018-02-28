*小程序分享或转发有两种方式，一种是通过在页面中自定义按钮的形式，另外一种只需要在js中定义 onShareAppMessage 函数，页面右上角就会出现转发的按钮。详细文档请参阅微信官方文档[微信转发API](https://mp.weixin.qq.com/debug/wxadoc/dev/api/share.html)。目前小程序好像暂不支持转发到微信朋友圈。*

效果图：
![sharePage.png](http://upload-images.jianshu.io/upload_images/4041074-7b51b5930755c8f4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) ![sharePage2.png](http://upload-images.jianshu.io/upload_images/4041074-4a5121ac00603d3a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)![shareFriends.png](http://upload-images.jianshu.io/upload_images/4041074-16d16392d639d0b8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### step1:在需要转发功能的wxml中定义一个button按钮，按钮的属性中加上open-type="share"。
示例代码：
```
<!--index.wxml-->
<view class='container'>
  <view class='card b-shadow'>
    <view class='card-content'>
      <image mode="widthFix"  src='../../images/benchi.png'></image> 
    </view>
    <view class='carDesc carDesc1'>
      <text>奔驰A230</text>
      <button class='share' id="shareBtn" open-type="share" type="primary" hover-class="other-button-hover">
        <image src='../../images/share.png'></image>
        分享
      </button>
    </view>
    <view class='carDesc carDesc2'>
      <text>梅赛德斯-奔驰旨在为消费者服务</text>
      <button  class='bg-c' type="primary" hover-class="other-button-hover">预约</button>
    </view>
  </view> 
</view>
```
###### step2:在js中加上onShareAppMessage函数 
示例代码：
 ```
  /**
* 用户点击右上角分享（index.js）
*/
  onShareAppMessage: function (ops) {
    if (ops.from === 'button') {
      // 来自页面内转发按钮
      console.log(ops.target)
    }
    return {
      title: 'xx小程序',
      path: 'pages/index/index',
      success: function (res) {
        // 转发成功
        console.log("转发成功:" + JSON.stringify(res));
      },
      fail: function (res) {
        // 转发失败
        console.log("转发失败:" + JSON.stringify(res));
      }
    }

  }
```
官方说明：
![share.png](http://upload-images.jianshu.io/upload_images/4041074-f3735623201ba329.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

