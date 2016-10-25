# ionic-ios-position-calc
IONIC混合开发IOS小坑之position定位计算区域问题


#《IONIC混合开发IOS小坑》
##position定位计算区域问题

###问题描述
* 安卓：头部横向导航条显示正常
* IOS：头部横向导航条上移
* 只有在打包成APP之后会有这个问题，用safari浏览器访问，不会出现这样的问题


![IOS](http://p1.bpimg.com/567571/38f595681eff195f.png)

###问题解决
* 个人发现这个IOS打包过后的导航条像是直接上移了一些像素，并不是position定位的问题，因为在解决问题的过程当中，尝试了position中的absolute，fixed，relative，实际上都没有解决问题。
* `position: relative;width: 100%;margin-top: 44px;z-index: 5;`当我把这个margin-top调整到64px的时候IOS的样式显示正常了。
* 也就是说IOS较安卓多计算了20个像素的高度。我估计是ionic 的框架将IOS的position定位在计算的时候把手机的消息通知栏高度给计算进去了。
* 于是也就有了解决问题的思路。
* 
`<div ng-class="{true: 'rn-index-scroll-ios', false: 'rn-index-scroll-android'}[isIOS]"></div>`
* `$scope.isIOS = isIos && pro;          //解决IOS导航兼容性问题`
* 这个校验的是UA和window.cordova,为true时，使用rn-index-scroll-ios样式。

###解决之后

![IOS](http://i1.piimg.com/567571/6109642c2e64ab2f.png)

###[APP下载地址](http://pre.im/yangnk)
