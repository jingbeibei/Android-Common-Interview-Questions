# Android-Common-Interview-Questions

>**面试题总结**

#通用
* 安卓学习途径, 寻找资料学习的博客网站  
* AndroidStudio使用, 插件使用  
* 安卓和苹果的区别  


#初级(基础1年左右)
* 四大组件  
* 五大存储方式  
* Layout布局有哪几种 FrameLayout什么时候用  
* ListView的优化  
* 点击事件设置监听的几种方式  
* 安卓主线程和子线程的关系  
* Activity生命周期 onStart onResume区别  
* Fragment生命周期 Activity和Fragment区别  
* 页面之间如何传递数据, 如果传递一个对象如何处理, 如何传递集合  
* dp px sp的区别  
* gravity和layout_gravity的区别  
* margin和padding的区别  
* weight的作用  
* Handler机制  
* 什么的ANR, 如何避免  
* 显式意图和隐式意图区别,隐式意图的使用  
* 广播几种接收方式, 广播有几种类型, 区别  
* 开启Service的几种方式, 区别, Service和Activity之间如何传递数据  
* Service中如果要start一个Activity要如何特殊处理,为什么  
...  
还有很多,都是网上常见面试题, 百度搜看看, 背下来即可  


#中级(2~3年, 也问部分基础问题)
* 自定义控件  
* 常用开源框架的使用  
* 动画类型  
* 任务栈,页面启动方式    
* Material Design / 新控件RecyclerView CardView等使用  
* 图片压缩和双缓存原理  
* 多层View的onTouch事件分发  
...   
简单了解记下来, 最好自己写个demo试验下


#高级(3年+, 也问部分中级问题)
* Android绘制原理 onMeasure onLayout onDraw作用  
* MeasureSpec的集中类型区别和作用  
* 自定义控件  
* 什么是MVC MVP,区别  
* 响应式编程  
* 常见开源框架源码  
* 单元测试常用框架和实际使用 场景  
...  
需要阅读源码和项目编码练习  

---

>其他

#多媒体
* 音频的环绕声和混响等如何处理  
* 音频录制播放  
* 视频的录制和播放  
* 播放使用的常用框架  
* Android原生支持格式  
* 软解码硬解码的区别  
* 如果要做一个按住屏幕右侧滑动调整声音功能如何处理  
...  
特殊公司做这方面相关的会问的多
---
###四大组件 
>Android四大组件分别为activity、service、content provider、broadcast receiver。
[常见AndRoid面试题第一篇：四大组件](http://www.jianshu.com/p/a5833ea6f044)

####1、activity
（1）一个Activity通常就是一个单独的屏幕（窗口）。
（2）Activity之间通过Intent进行通信。
（3）android应用中每一个Activity都必须要在AndroidManifest.xml配置文件中声明，否则系统将不识别也不执行该Activity。
####2、service
（1）service用于在后台完成用户指定的操作。service分为两种：

（a）started（启动）：当应用程序组件（如activity）调用startService()方法启动服务时，服务处于started状态。

（b）bound（绑定）：当应用程序组件调用bindService()方法绑定到服务时，服务处于bound状态。

（2）startService()与bindService()区别：

（a）started service（启动服务）是由其他组件调用startService()方法启动的，这导致服务的onStartCommand()方法被调用。当服务是started状态时，其生命周期与启动它的组件无关，并且可以在后台无限期运行，即使启动服务的组件已经被销毁。因此，服务需要在完成任务后调用stopSelf()方法停止，或者由其他组件调用stopService()方法停止。

（b）使用bindService()方法启用服务，调用者与服务绑定在了一起，调用者一旦退出，服务也就终止，大有“不求同时生，必须同时死”的特点。

（3）开发人员需要在应用程序配置文件中声明全部的service，使用<service></service>标签。

（4）Service通常位于后台运行，它一般不需要与用户交互，因此Service组件没有图形用户界面。Service组件需要继承Service基类。Service组件通常用于为其他组件提供后台服务或监控其他组件的运行状态。

####3、content provider
（1）android平台提供了Content Provider使一个应用程序的指定数据集提供给其他应用程序。其他应用可以通过ContentResolver类从该内容提供者中获取或存入数据。

（2）只有需要在多个应用程序间共享数据是才需要内容提供者。例如，通讯录数据被多个应用程序使用，且必须存储在一个内容提供者中。它的好处是统一数据访问方式。

（3）ContentProvider实现数据共享。ContentProvider用于保存和获取数据，并使其对所有应用程序可见。这是不同应用程序间共享数据的唯一方式，因为android没有提供所有应用共同访问的公共存储区。

（4）开发人员不会直接使用ContentProvider类的对象，大多数是通过ContentResolver对象实现对ContentProvider的操作。

（5）ContentProvider使用URI来唯一标识其数据集，这里的URI以content://作为前缀，表示该数据由ContentProvider来管理。

####4、broadcast receiver
（1）你的应用可以使用它对外部事件进行过滤，只对感兴趣的外部事件(如当电话呼入时，或者数据网络可用时)进行接收并做出响应。广播接收器没有用户界面。然而，它们可以启动一个activity或serice来响应它们收到的信息，或者用NotificationManager来通知用户。通知可以用很多种方式来吸引用户的注意力，例如闪动背灯、震动、播放声音等。一般来说是在状态栏上放一个持久的图标，用户可以打开它并获取消息。

（2）广播接收者的注册有两种方法，分别是程序动态注册和AndroidManifest文件中进行静态注册。

（3）动态注册广播接收器特点是当用来注册的Activity关掉后，广播也就失效了。静态注册无需担忧广播接收器是否被关闭，只要设备是开启状态，广播接收器也是打开着的。也就是说哪怕app本身未启动，该app订阅的广播在触发时也会对它起作用。

####总结
（1）4大组件的注册

4大基本组件都需要注册才能使用，每个Activity、service、Content Provider都需要在AndroidManifest文件中进行配置。AndroidManifest文件中未进行声明的activity、服务以及内容提供者将不为系统所见，从而也就不可用。而broadcast receiver广播接收者的注册分静态注册（在AndroidManifest文件中进行配置）和通过代码动态创建并以调用Context.registerReceiver()的方式注册至系统。需要注意的是在AndroidManifest文件中进行配置的广播接收者会随系统的启动而一直处于活跃状态，只要接收到感兴趣的广播就会触发（即使程序未运行）。

（2）4大组件的激活

内容提供者的激活：当接收到ContentResolver发出的请求后，内容提供者被激活。而其它三种组件activity、服务和广播接收器被一种叫做intent的异步消息所激活。

（3）4大组件的关闭

内容提供者仅在响应ContentResolver提出请求的时候激活。而一个广播接收器仅在响应广播信息的时候激活。所以，没有必要去显式的关闭这些组件。
Activity关闭：可以通过调用它的finish()方法来关闭一个activity。
服务关闭：对于通过startService()方法启动的服务要调用Context.stopService()方法关闭服务，使用bindService()方法启动的服务要调用Contex.unbindService()方法关闭服务。

（4）android中的任务（activity栈）

（a）任务其实就是activity的栈，它由一个或多个Activity组成，共同完成一个完整的用户体验。栈底的是启动整个任务的Activity，栈顶的是当前运行的用户可以交互的Activity，当一个activity启动另外一个的时候，新的activity就被压入栈，并成为当前运行的activity。而前一个activity仍保持在栈之中。当用户按下BACK键的时候，当前activity出栈，而前一个恢复为当前运行的activity。栈中保存的其实是对象，栈中的Activity永远不会重排，只会压入或弹出。

（b）任务中的所有activity是作为一个整体进行移动的。整个的任务（即activity栈）可以移到前台，或退至后台。

（c）Android系统是一个多任务(Multi-Task)的操作系统，可以在用手机听音乐的同时，也执行其他多个程序。每多执行一个应用程序，就会多耗费一些系统内存，当同时执行的程序过多，或是关闭的程序没有正确释放掉内存，系统就会觉得越来越慢，甚至不稳定。为了解决这个问题，Android引入了一个新的机制，即生命周期(Life Cycle)。[原文链接](http://www.jianshu.com/p/930dadb7a3cf)

---
###五大存储方式
>[Android平台中实现数据存储的5种方式](http://www.cnblogs.com/hanyonglu/archive/2012/03/01/2374894.html)

数据存储在开发中是使用最频繁的，在这里主要介绍Android平台中实现数据存储的5种方式，分别是：

 1 使用SharedPreferences存储数据

 2 文件存储数据

 3 SQLite数据库存储数据

 4 使用ContentProvider存储数据

 5 网络存储数据

**第一种：使用SharedPreferences存储数据**

SharedPreferences是Android平台上一个轻量级的存储类，主要是保存一些常用的配置比如窗口状态，一般在Activity中 重载窗口状态onSaveInstanceState保存一般使用SharedPreferences完成，它提供了Android平台常规的Long长 整形、Int整形、String字符串型的保存。 

 它是什么样的处理方式呢? SharedPreferences类似过去Windows系统上的ini配置文件，但是它分为多种权限，可以全局共享访问，android123提示最终是以xml方式来保存，整体效率来看不是特别的高，对于常规的轻量级而言比SQLite要好不少，如果真的存储量不大可以考虑自己定义文件格式。xml 处理时Dalvik会通过自带底层的本地XML Parser解析，比如XMLpull方式，这样对于内存资源占用比较好。

  它的本质是基于XML文件存储key-value键值对数据，通常用来存储一些简单的配置信息。

 其存储位置在/data/data/<包名>/shared_prefs目录下。

 SharedPreferences对象本身只能获取数据而不支持存储和修改，存储修改是通过Editor对象实现。

 实现SharedPreferences存储的步骤如下： 　　

1）、根据Context获取SharedPreferences对象 　　

2）、利用edit()方法获取Editor对象。 　　

3）、通过Editor对象存储key-value键值对数据。 　　

4）、通过commit()方法提交数据。

```
public class MainActivity extends Activity {'
 @Override
 public void onCreate(Bundle savedInstanceState) {
 super.onCreate(savedInstanceState);
 setContentView(R.layout.main);
  
 //获取SharedPreferences对象
 Context ctx = MainActivity.this; 
 SharedPreferences sp = ctx.getSharedPreferences("SP", MODE_PRIVATE);
 //存入数据
 Editor editor = sp.edit();
 editor.putString("STRING_KEY", "string");
 editor.putInt("INT_KEY", 0);
 editor.putBoolean("BOOLEAN_KEY", true);
 editor.commit();
  
 //返回STRING_KEY的值
 Log.d("SP", sp.getString("STRING_KEY", "none"));
 //如果NOT_EXIST不存在，则返回值为"none"
 Log.d("SP", sp.getString("NOT_EXIST", "none"));
 }
}
```
这段代码执行过后，即在/data/data/com.test/shared_prefs目录下生成了一个SP.xml文件，一个应用可以创建多个这样的xml文件。 

 SharedPreferences对象与SQLite数据库相比，免去了创建数据库，创建表，写SQL语句等诸多操作，相对而言更加方便，简洁。但是SharedPreferences也有其自身缺陷，比如其职能存储boolean，int，float，long和String五种简单的数据类型，比如其无法进行条件查询等。所以不论SharedPreferences的数据存储操作是如何简单，它也只能是存储方式的一种补充，而无法完全替代如SQLite数据库这样的其他数据存储方式。

**第二种：文件存储数据**
关于文件存储，Activity提供了openFileOutput()方法可以用于把数据输出到文件中，具体的实现过程与在J2SE环境中保存数据到文件中是一样的。

 文件可用来存放大量数据，如文本、图片、音频等。

 默认位置：/data/data/<包>/files/***.***。 
```
public void save()
{
 
try {
FileOutputStream outStream=this.openFileOutput("a.txt",Context.MODE_WORLD_READABLE);
outStream.write(text.getText().toString().getBytes());
outStream.close();
Toast.makeText(MyActivity.this,"Saved",Toast.LENGTH_LONG).show();
} catch (FileNotFoundException e) {
return;
}
catch (IOException e){
return ;
}
} 

```
openFileOutput()方法的第一参数用于指定文件名称，不能包含路径分隔符“/” ，如果文件不存在，Android 会自动创建它。

 创建的文件保存在/data/data/<package name>/files目录，如： /data/data/cn.itcast.action/files/itcast.txt ，通过点击Eclipse菜单“Window”-“Show View”-“Other”，在对话窗口中展开android文件夹，选择下面的File Explorer视图，然后在File Explorer视图中展开/data/data/<package name>/files目录就可以看到该文件。 

 openFileOutput()方法的第二参数用于指定操作模式，有四种模式，分别为：

 Context.MODE_PRIVATE = 0

 Context.MODE_APPEND = 32768

 Context.MODE_WORLD_READABLE = 1

 Context.MODE_WORLD_WRITEABLE = 2

 Context.MODE_PRIVATE：为默认操作模式，代表该文件是私有数据，只能被应用本身访问，在该模式下，写入的内容会覆盖原文件的内容，如果想把新写入的内容追加到原文件中。可以使用Context.MODE_APPEND

 Context.MODE_APPEND：模式会检查文件是否存在，存在就往文件追加内容，否则就创建新文件。

 Context.MODE_WORLD_READABLE和Context.MODE_WORLD_WRITEABLE用来控制其他应用是否有权限读写该文件。

 MODE_WORLD_READABLE：表示当前文件可以被其他应用读取；

 MODE_WORLD_WRITEABLE：表示当前文件可以被其他应用写入。

 如果希望文件被其他应用读和写，可以传入： openFileOutput("itcast.txt", Context.MODE_WORLD_READABLE + Context.MODE_WORLD_WRITEABLE); android有一套自己的安全模型，当应用程序(.apk)在安装时系统就会分配给他一个userid，当该应用要去访问其他资源比如文件的时候，就需要userid匹配。默认情况下，任何应用创建的文件，sharedpreferences，数据库都应该是私有的（位于/data/data/<package name>/files），其他程序无法访问。

 除非在创建时指定了Context.MODE_WORLD_READABLE或者Context.MODE_WORLD_WRITEABLE ，只有这样其他程序才能正确访问。
读取文件示例：
```
public void load()
{
 try {
 FileInputStream inStream=this.openFileInput("a.txt");
 ByteArrayOutputStream stream=new ByteArrayOutputStream();
 byte[] buffer=new byte[1024];
 int length=-1;
 while((length=inStream.read(buffer))!=-1) {
 stream.write(buffer,0,length);
 }
 
 
 stream.close();
 inStream.close();
 text.setText(stream.toString());
 Toast.makeText(MyActivity.this,"Loaded",Toast.LENGTH_LONG).show();
 } catch (FileNotFoundException e) {
 e.printStackTrace();
 }
 catch (IOException e){
 return ;
 }
 
} 

```
对于私有文件只能被创建该文件的应用访问，如果希望文件能被其他应用读和写，可以在创建文件时，指定Context.MODE_WORLD_READABLE和Context.MODE_WORLD_WRITEABLE权限。  

 Activity还提供了getCacheDir()和getFilesDir()方法： getCacheDir()方法用于获取/data/data/<package name>/cache目录 getFilesDir()方法用于获取/data/data/<package name>/files目录。

 把文件存入SDCard：

 使用Activity的openFileOutput()方法保存文件，文件是存放在手机空间上，一般手机的存储空间不是很大，存放些小文件还行，如果要存放像视频这样的大文件，是不可行的。对于像视频这样的大文件，我们可以把它存放在SDCard。 

 SDCard是干什么的？你可以把它看作是移动硬盘或U盘。 在模拟器中使用SDCard，你需要先创建一张SDCard卡（当然不是真的SDCard，只是镜像文件）。

 创建SDCard可以在Eclipse创建模拟器时随同创建，也可以使用DOS命令进行创建，如下： 在Dos窗口中进入android SDK安装路径的tools目录，输入以下命令创建一张容量为2G的SDCard，文件后缀可以随便取，建议使用.img： mksdcard 2048M D:\AndroidTool\sdcard.img 在程序中访问SDCard，你需要申请访问SDCard的权限。

 在AndroidManifest.xml中加入访问SDCard的权限如下:
```
<!-- 在SDCard中创建与删除文件权限 -->
<uses-permission android:name="android.permission.MOUNT_UNMOUNT_FILESYSTEMS"/>
 
<!-- 往SDCard写入数据权限 -->
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/> 
 
```

要往SDCard存放文件，程序必须先判断手机是否装有SDCard，并且可以进行读写。
注意：访问SDCard必须在AndroidManifest.xml中加入访问SDCard的权限。
```
if(Environment.getExternalStorageState().equals(Environment.MEDIA_MOUNTED)){ 
 File sdCardDir = Environment.getExternalStorageDirectory();//获取SDCard目录 
 
 File saveFile = new File(sdCardDir, “a.txt”);
 FileOutputStream outStream = new FileOutputStream(saveFile);
 outStream.write("test".getBytes());
 outStream.close();
}

```
Environment.getExternalStorageState()方法用于获取SDCard的状态，如果手机装有SDCard，并且可以进行读写，那么方法返回的状态等于Environment.MEDIA_MOUNTED。 

 Environment.getExternalStorageDirectory()方法用于获取SDCard的目录，当然要获取SDCard的目录，你也可以这样写：
```
File sdCardDir = new File("/sdcard"); //获取SDCard目录
File saveFile = new File(sdCardDir, "itcast.txt");
//上面两句代码可以合成一句：
File saveFile = new File("/sdcard/a.txt");
FileOutputStream outStream = new FileOutputStream(saveFile);
outStream.write("test".getBytes());
outStream.close(); 

```
**第三种SQLite数据库存储数据**

SQLite是轻量级嵌入式数据库引擎，它支持 SQL 语言，并且只利用很少的内存就有很好的性能。此外它还是开源的，任何人都可以使用它。许多开源项目（(Mozilla, PHP, Python）都使用了 SQLite.SQLite 由以下几个组件组成：SQL 编译器、内核、后端以及附件。SQLite 通过利用虚拟机和虚拟数据库引擎（VDBE），使调试、修改和扩展 SQLite 的内核变得更加方便。
特点：
* 面向资源有限的设备；
* 没有服务器进程；
* 所有数据存放在同一文件中跨平台；
* 可自由复制。 
**第四种：使用ContentProvider存储数据**
Android这个系统和其他的操作系统还不太一样，我们需要记住的是，数据在Android当中是私有的，当然这些数据包括文件数据和数据库数据以及一些其他类型的数据。那这个时候有读者就会提出问题，难道两个程序之间就没有办法对于数据进行交换？Android这么优秀的系统不会让这种情况发生的。解决这个问题主要靠ContentProvider。一个Content Provider类实现了一组标准的方法接口，从而能够让其他的应用保存或读取此Content Provider的各种数据类型。也就是说，一个程序可以通过实现一个Content Provider的抽象接口将自己的数据暴露出去。外界根本看不到，也不用看到这个应用暴露的数据在应用当中是如何存储的，或者是用数据库存储还是用文件存储，还是通过网上获得，这些一切都不重要，重要的是外界可以通过这一套标准及统一的接口和程序里的数据打交道，可以读取程序的数据，也可以删除程序的数据，当然，中间也会涉及一些权限的问题。 

 一个程序可以通过实现一个ContentProvider的抽象接口将自己的数据完全暴露出去，而且ContentProviders是以类似数据库中表的方式将数据暴露，也就是说ContentProvider就像一个“数据库”。那么外界获取其提供的数据，也就应该与从数据库中获取数据的操作基本一样，只不过是采用URI来表示外界需要访问的“数据库”。 

 Content Provider提供了一种多应用间数据共享的方式，比如：联系人信息可以被多个应用程序访问。

 Content Provider是个实现了一组用于提供其他应用程序存取数据的标准方法的类。 应用程序可以在Content Provider中执行如下操作: 查询数据 修改数据 添加数据 删除数据

 标准的Content Provider: Android提供了一些已经在系统中实现的标准Content Provider，比如联系人信息，图片库等等，你可以用这些Content Provider来访问设备上存储的联系人信息，图片等等。

**第五种：网络存储数据**
前面介绍的几种存储都是将数据存储在本地设备上，除此之外，还有一种存储（获取）数据的方式，通过网络来实现数据的存储和获取。

 我们可以调用WebService返回的数据或是解析HTTP协议实现网络数据交互。

 具体需要熟悉java.net.*，Android.net.*这两个包的内容，在这就不赘述了，请大家参阅相关文档。

---
###Layout布局有哪几种 FrameLayout什么时候用
>[Android五大布局介绍&属性设置大全](http://www.jianshu.com/p/4fac6304d872)

在Android中，共有五种布局方式，分别是：
* FrameLayout(框架布局)
* LinearLayout(线性布局)
* AbsoluteLayout(绝对布局)
* RelativeLayout(相对布局)
* TableLayout(表格布局)

**1. FrameLayout框架布局**
布局特点：放入其中的所有元素都被放置在最左上的区域，而且无法为这些元素指定一个确切的位置,下一个子元素会重叠覆盖上一个子元素
应用场景：适合浏览单张图片。

**2. LinearLayout线性布局**
布局特点：放主要提供控件水平或者垂直排列的模型，每个子组件都是以垂直或水平的方式来线性排布.(默认是垂直)
应用场景：最常用的布局方式linearLayout中有一个重要的属性 android:layout_weight="1"，这个weight在垂直布局时，代表行距；水平的时候代表列宽；weight值越大就越大。

**3. AbsoluteLayout绝对定位布局**
布局特点：采用坐标轴的方式定位组件，左上角是（0，0）点，往右x轴递增，往下Y轴递增,组件定位属性为android:layout_x和 android:layout_y来确定坐标。
应用场景：准确定位空间位置由于Android手机的屏幕尺寸、分辨率存在较大差异，使用AbsoluteLayout无法兼顾适配问题，所以该布局已经过时

**4. RelativeLayout相对布局**
布局特点：为某一个组件为参照物，来定位下一个组件的位置的布局方式。
应用场景：控件之间存在相应关系（适配神器，推荐使用）

**5. TableLayout表格布局**
布局特点：类似Html里的Table.使用TableRow来布局，其中TableRow代表一行，TableRow的每一个视图组件代表一个单元格。
应用场景：控件之间存在相应关系。

---
###ListView的优化 
