# Android-common-sense
Android common sense (notes).It is a base note for myself to android develop

### 关于dp，dip，dpi，px，sp，以及layout-xxxdpi和layout-xxxdp的简单记录。
======

  1、dpi（dot per inch）,即每英寸像素，所有的android设备都会被分成120（low）,160(medium),240(high),320(xhigh)四种，后来随着市场上android设备越来越多，google官方又增加了213（Added in API level13）,480（Added in API level16）,640（Added in API level18）,三种dpi。比如320*240分辨率的屏幕物理尺寸2英寸*1.5英寸，dpi=160；
  
  2、dp或dip（density-independent pixel）逻辑密度计算单位，与像素的换算方式为px=dp*（dpi/160）。
  
  以上是我看到一个认为比较好的介绍。在这个基础上我也记录一下我自己对这个的认识。每部手机屏幕长宽值是固定。相同的屏幕下的像素值越多，越是清晰。宽（长）像素值/宽（长）逻辑密度计算单位，px/dp=density。density =getWindowManager().getDefaultDisplay().getMetrics(DisplayMetrics())。相信这个公式大家还是很清楚的。没错这个就是我们常用的px，dp换算的方法。我是这样理解这个公式的。我们要确保每个屏幕分辨率下所展示的view效果出入不大，需要根据屏幕的具体分辨率来处理。好比两部手机屏幕大小一样，但是手机分辨率却有差异。一部是800*480的，另一部是1280*900（这里指的是像素）。代码中设置view的长和宽为80，运行后发现两部手机显示出来的内容不一样。好像1280*900的view要小不少。没错，这就是像素密度不同的结果。值得一提的是代码中设置view的时候，80被定义的单位是px。然而我们希望手机展示出来的效果一样，那有该怎么办呢？没错，我们应该将80的单位理解为dp然后根据不同手机的分辨率密度density来转换成相应的px。这样一来虽然初始化的像素值不同，但展现出来的效果却是我们想要的。这也是屏幕适配的一种解决方案。
  
  在android3.2以前，所有的资源文件都有相应的xhdpi,hdpi,mdpi,ldpi四种文件来对应，android3.2以后，为了提供更精准的对布局文件的控制，可以通过为资源文件（res目录下文件）增加后缀来指定该文件夹里的xml布局文件或color.xml，string.xml是为哪种大小的屏幕使用。
  
第一种后缀：sw<N>dp,如layout-sw600dp, values-sw600dp
  这里的sw代表smallwidth的意思，当你所有屏幕的最小宽度都大于600dp时,屏幕就会自动到带sw600dp后缀的资源文件里去寻找相关资源文件，这里的最小宽度是指屏幕宽高的较小值，每个屏幕都是固定的，不会随着屏幕横向纵向改变而改变。
  
第二种后缀w<N>dp 如layout-w600dp, values-w600dp
  带这样后缀的资源文件的资源文件制定了屏幕宽度的大于Ndp的情况下使用该资源文件，但它和sw<N>dp不同的是，当屏幕横向纵向切换时，屏幕的宽度是变化的，以变化后的宽度来与N相比，看是否使用此资源文件下的资源。
  
第三种后缀h<N>dp 如layout-h600dp, values-h600dp
  这个后缀的使用方式和w<N>dp一样，随着屏幕横纵向的变化，屏幕高度也会变化，根据变化后的高度值来判断是否使用h<N>dp ，但这种方式很少使用，因为屏幕在纵向上通常能够滚动导致长度变化，不像宽度那样基本固定，因为这个方法灵活性不是很好，google官方文档建议尽量少使用这种方式。
  
###### ps:以上为个人帮助记忆的note，若有不当的理解希望不会误导他人。
  
###### ps2：部分内容有借用，没有贴出链接是因为我也不清楚他是否为原帖，请原帖主人多见谅。
