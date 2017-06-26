# iTween 基本原理
* iTween是数值插件，iTween的核心是数值插值，简单说就是给iTween两个数值(开始值，结束值)，它会自动生成一些中间值，大概像这样子, 开始值->中间值 -> 中间值 …. -> 结束值。
* 这里的数值可以理解为: 数字，坐标点，角度，物体大小，物体颜色，音量大小 等
# iTween类的介绍
* 可分为三大类：
1. 静态注册方法：提供注册动画效果的静态方法接口。如：MoveTo、CameraFadeTo等。
2. Update静态方法：提供注册每帧改变属性值的环境，在Update或循环环境中调用。如：MoveUpdate、AudioUpdate等。
3. 外部工具方法：包括动画控制、路径绘制等。
### iTween类内部定义了三种枚举类型：
1. EaseType：缓动类型枚举
2. LoopType：动画的循环类型枚举
3. NamedValueColor:已命名颜色枚举
# iTween的主要功能介绍
* 有八大实现动画方法：
1. Fade：淡入淡出
2. Look：旋转对象使其面朝指定位置
3. Move：移动位置
4. Rotate：旋转指定欧拉角度
5. Scale：缩放大小
6. Punch：添加摇晃力
7. Shake：摆动对象
8. CameraFade：摄像机的淡入淡出
* 两种音频方法：
1. Audio：音量和音调的变化
2. Stab ：播放AudioClip一次，不用手动加载AudioSource组件
* 一种颜色变化方法：
1. Color：变换颜色
* 一种值变化方法
1. ValueTo：返回一个“from”和“to”之间的插值，用以改变属性
* **每个方法一般有两种重载方式：最小定制选项、完全定制项。
