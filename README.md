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
>[Android中ListView常见优化方案](http://www.jianshu.com/p/728e031f1a74)

* 一、复用convertView，减少findViewById的次数
* 二、缓存item条目的引用——ViewHolder
  ViewHolder模式 充分利用了视图的缓存机制 避免了每次调用getView()时候都去通过findViewById实例化控件
* 三、给listView设置滚动监听器 根据不同状态 不同处理数据 分批分页加载 根据listView的状态去操作
* 四、listview每个item层级结构不要太复杂
* 五、如果listview每个item要加载图片 一定要对图片的加载进行优化。
* 六、避免在listview适配器中使用线程
* 七、ScrollView 和listview 会有冲突
* 八、避免在getView方法中做耗时操作
---

###点击事件设置监听的几种方式
**方法一：写一个内部类，在类中实现点击事件**
```
bt_dail.setOnClickListener(new MyButtonListener());
private class MyButtonListener implements OnClickListener{
/**
 * 当按钮被点击的时候调用
 */
@Override
public void onClick(View v) {
     callPhone();
}
}
```
**方法二：匿名内部类**
```
bt_dail.setOnClickListener(new OnClickListener() {
@Override
public void onClick(View v) {
   callPhone();
}
});
```
**方法三：让activity实现点击接口**
```
public class MainActivity extends Activity implements OnClickListener 
//调用点击事件方法
bt_dail.setOnClickListener(this);
//实现接口
@Override
public void onClick(View v) {
        switch (v.getId()) {
                   case R.id.bt_dail:
                            callPhone();
                            break;
                 default:
                 break;
        }
}
```
**方法四：在layout文件中定义button点击时调用的方法**
```
<Button        
android:id="@+id/bt_dail" 
android:layout_width="wrap_content"
android:layout_height="wrap_content"        
android:onClick="dailPhone"        
android:text="拨打此号码" />
定义方法：
public void dailPhone(View view){  
    callPhone();  
} 
```
**方法五：外部内做事件监听**
就是另外创建一个处理事件的Java文件,这种形式用的比较少！因为外部类不能直接访问用户界面类中的组件,要通过构造方法将组件传入使用;这样导致的结果就是代码不够简洁！

---
###安卓主线程和子线程的关系
> * **主线程**：也叫UI线程，或称ActivityThread，用于运行四大组件和处理他们用户的交互。 ActivityThread管理应用进程的主线程的执行(相当于普通Java程序的main入口函数)，在Android系统中，在默认情况下，一个应用程序内的各个组件(如Activity、BroadcastReceiver、Service)都会在同一个进程(Process)里执行，且由此进程的主线程负责执行。ActivityThread既要处理Activity组件的UI事件，又要处理Service后台服务工作，通常会忙不过来。为了解决此问题，主线程可以创建多个子线程来处理后台服务工作，而本身专心处理UI画面的事件。

>*  **子线程**： 用于执行耗时操作，比如 I/O操作和网络请求等。（安卓3.0以后要求耗访问网络必须在子线程种执行）更新UI的工作必须交给主线程，子线程在安卓里是不允许更新UI的。

Android是单线程模型，我们创建的Service、Activity以及Broadcast均是在一个主线程处理，这里我们可以理解为UI线程。
      但是在操作一些耗时操作时，比如I/O读写的大文件读写，数据库操作以及网络下载需要很长时间，为了不阻塞用户界面，出现ANR的响应提示窗口，这个时候我们考虑使用Thread线程来解决。

  1. 任何耗时的处理过程都会降低用户界面的响应速度，甚至导致用户界面失去响应，当用户界面失去响应超过5秒钟，Android系统会允许用户强行关闭应用程序。
![](http://upload-images.jianshu.io/upload_images/2314135-08276baa23cc99fe.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
  2. 较好的解决方法是将耗时的处理过程转移到子线程上，这样可以避免负责界面更新的主线程无法处理界面事件，从而避免用户界面长时间失去响应。
  3. 线程是独立的程序单元，多个线程可以并行工作。
  4. 在多处理器系统中，每个中央处理器（CPU）单独运行一个线程，因此线程是并行工作的。
  5.  在单处理器系统中，处理器会给每个线程一小段时间，在这个时间内线程是被执行的，然后处理器执行下一个线程，这样就产生了线程并行运行的假象。
  6. 无论线程是否真的并行工作，在宏观上可以认为子线程是独立于主线程，且能与主线程并行工作的程序单元。
  7. Android中的线程是基于Java定义的线程,其内部结构如图所示：
![](http://upload-images.jianshu.io/upload_images/2314135-efe94bd24674aa85.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

  8. 一个应用程序中可能会包含多个线程（Ｔｈｒｅａｄ），每个线程中都有一个run()方法，run()方法内部的程序执行完毕后，所在的线程就自动结束。
  9. 每个线程都有一个消息队列，用于不同的线程之间传递消息。在run()方法内部，如果不主动去读取消息队列中的消息，这些消息就是一些无用的消息，因为它们没有被处理。
  10. 在Android系统中，读取消息和处理消息是两个步骤，并由两个不同的部分完成，先读取消息，然后才能处理消息。
  11. 无论是本线程的还是其它线程，都不能直接处理消息队列中的消息，而是需要通过在线程内部定义一个Handler类对象来处理消息队列。一个Thread只能包含一个Handler对象。在实际应用中，读取消息队列一般需要循环执行，即不断地从消息队列中获取消息并进行相应处理，这就又需要一个Looper对象。
  12. Looper对象用于循环读取消息队列的值，并回调Handler对象中定义的消息处理函数，同时，Looper对象还可以将读取的消息从队列中移除，执行完一次消息处理后，再循环从消息队列中读取下一个消息，直到Looper对象调用stop()方法退出循环。如果消息队列中没有消息，Looper对象则会等待，线程不会退出。
  13. 为了更方便地从线程中使用Looper功能，Android又定义了一个HandlerThread类，该类基于Thread，并且内部已经添加了Looper功能，使用者只需重写其onLooperPrepared ()方法，添加具体应用代码即可。Android中一个Activity就是一个线程，多个Activity之间的切换是在同一个线程中。
文／SingleoD（简书作者）[原文链接](http://www.jianshu.com/p/7307492f7e89)
---
###Activity生命周期 onStart onResume区别
首先了解Activity的四种状态
Running状态：一个新的Activity启动入栈后，它在屏幕最前端，处于栈的最顶端，此时它处于可见并可和用户交互的激活状态。Paused状态：当Activity被另一个透明或者Dialog样式的Activity覆盖时的状态。此时它依然与窗口管理器保持连接，系统继续维护其内部状态，它仍然可见，但它已经失去了焦点，故不可与用户交互。Stopped状态：当Activity不可见时，Activity处于Stopped状态。当Activity处于此状态时，一定要保存当前数据和当前的UI状态，否则一旦Activity退出或关闭时，当前的数据和UI状态就丢失了。Killed状态：Activity被杀掉以后或者被启动以前，处于Killed状态。这是Activity已从Activity堆栈中移除，需要重新启动才可以显示和使用。
4种状态中，Running状态和Paused状态是可见的，Stopped状态和Killed状态时不可见的。
 
onStart()和onResume()的区别

onStart()是activity界面被显示出来的时候执行的，用户可见，包括有一个activity在他上面，但没有将它完全覆盖，用户可以看到部分activity但不能与它交互
onResume()是当该activity与用户能进行交互时被执行，用户可以获得activity的焦点，能够与用户交互。

onStart()通常就是onStop()（也就是用户按下了home键，activity变为后台后），之后用户再切换回这个activity就会调用onRestart()而后调用onStart()
onResume()是onPause()（通常是当前的acitivty被暂停了，比如被另一个透明或者Dialog样式的Activity覆盖了），之后dialog取消，activity回到可交互状态，调用onResume()。


![Paste_Image.png](http://upload-images.jianshu.io/upload_images/2314135-e24a86bed77d1705.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
引申：经测试，onPause()方法在弹出Dialog时不会被调用，而在被另一个透明或者Dialog样式的Activity覆盖时才会被调用。
附activity生命周期：

![Paste_Image.png](http://upload-images.jianshu.io/upload_images/2314135-95b9dc3f4c620691.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---
###Fragment生命周期 Activity和Fragment区别
**Activity生命周期图：**
```onCreate()：创建时调用
onStart()：可见时调用
onResume()：获取焦点时用
onPause()：失去焦点时调用
onStop()：不可见时调用
onRestart()：重启时调用
onDestory()：销毁时调用```

![activity.png](http://upload-images.jianshu.io/upload_images/2314135-57591e25232d1410.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
**Fragment生命周期：**
```
onAttach()：和宿主Activity建立关联时调用
onCreate()：创建时调用
onCreateView()：加载Fragment的布局时调用
onActivityCreated()：宿主Activity创建完毕时调用
onStart()：可见时调用
onResume()：获取焦点时用
onPause()：失去焦点时调用
onStop()：不可见时调用
onDestoryView()：移除Fragment的布局时调用
onDestory()：销毁时调用
onDetach()：与宿主Activity解除关联时调用

```
![Fragment.png](http://upload-images.jianshu.io/upload_images/2314135-156a9aaa667b4ab5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
**Fragment与Activity生命周期对比图：**

![Paste_Image.png](http://upload-images.jianshu.io/upload_images/2314135-bae480de789f439c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
**Fragment生命周期分析：**
1. 当一个fragment被创建的时候，它会经历以下状态.
onAttach()
onCreate()
onCreateView()
onActivityCreated()

2. 当这个fragment对用户可见的时候，它会经历以下状态。
onStart()
onResume()

3. 当这个fragment进入“后台模式”的时候，它会经历以下状态。
onPause()
onStop()

4. 当这个fragment被销毁了（或者持有它的activity被销毁了），它会经历以下状态。
onPause()
onStop()
onDestroyView()
onDestroy() // 本来漏掉类这个回调，感谢xiangxue336提出。
onDetach()

5. 就像activitie一样，在以下的状态中，可以使用Bundle对象保存一个fragment的对象。
onCreate()
onCreateView()
onActivityCreated()

6. fragments的大部分状态都和activitie很相似，但fragment有一些新的状态。
onAttached() —— 当fragment被加入到activity时调用（在这个方法中可以获得所在的activity）。
onCreateView() —— 当activity要得到fragment的layout时，调用此方法，fragment在其中创建自己的layout(界面)。
onActivityCreated() —— 当activity的onCreated()方法返回后调用此方法
onDestroyView() —— 当fragment中的视图被移除的时候，调用这个方法。
onDetach() —— 当fragment和activity分离的时候，调用这个方法。

一旦activity进入resumed状态（也就是running状态），你就可以自由地添加和删除fragment了。因此，只有当activity在resumed状态时，fragment的生命周期才能独立的运转，其它时候是依赖于activity的生命周期变化的。

**Activity生命周期分析：**
上面7个生命周期方法分别在4个阶段按着一定的顺序进行调用，这4个阶段如下：
 开始Activity：在这个阶段依次执行3个生命周期方法：onCreate、onStart和onResume。
 Activity失去焦点：如果在Activity获得焦点的情况下进入其他的Activity或应用程序，这时当前的Activity会失去焦点。在这一阶段，会依次执行onPause和onStop方法。
Activity重新获得焦点：如果Activity重新获得焦点，会依次执行3个生命周期方法：onRestart、onStart和onResume。
 关闭Activity：当Activity被关闭时系统会依次执行3个生命周期方法：onPause、onStop和onDestroy。

 如果在这4个阶段执行生命周期方法的过程中不发生状态的改变，那么系统会按着上面的描述依次执行这4个阶段中的生命周期方法，但如果在执行的过程中改变了状态，系统会按着更复杂的方式调用生命周期方法。

在执行的过程中可以改变系统的执行轨迹的生命周期方法是onPause和onStop。如果在执行onPause方法的过程中Activity重新获得了焦点，然后又失去了焦点。系统将不会再执行onStop方法，而是按着如下的顺序执行相应的生命周期方法：onPause -> onResume-> onPause

如果在执行onStop方法的过程中Activity重新获得了焦点，然后又失去了焦点。系统将不会执行onDestroy方法，而是按着如下的顺序执行相应的生命周期方法：
onStop -> onRestart -> onStart -> onResume -> onPause -> onStop

 在图Activity生命周期里可以看出，系统在终止应用程序进程时会调用onPause、onStop和onDesktroy方法。而onPause方法排在了最前面，也就是说，Activity在失去焦点时就可能被终止进程，而onStop和onDestroy方法可能没有机会执行。因此，应该在onPause方法中保存当前Activity状态，这样才能保证在任何时候终止进程时都可以执行保存Activity状态的代码.

---
###页面之间如何传递数据, 如果传递一个对象如何处理, 如何传递集合
* 1.简单数据
   通过intent.putExtra("key","value")方法，在第二个界面中用getIntent()方法获取启动当前activity的intent，然后调用intent的getStringExtra()方法来获取传的数据，如果传递的是整型，则用getIntExtra()方法来获取，如果传的是布尔型，则用getBooleanExtra()方法，以此类推。
通过Bundle,bundle.putString("key","value"),intnet.putExtras(bundle),
在第二个activity中获取bundle:getIntent().getExtras();
接收参数s=bundle.getString("key")
* 2.集合
```
bundle.putParcelableArrayList("list",bundlelist);
//接收参数
list = bundle.getParcelableArrayList("list");
```
* 3.对象
*1.通过实现Serializable接口 *
      bundleSerializable.putSerializable("serializable", map2)
      //接收参数
      bundle.getSerializable("serializable");
*2.通过实现Parcelable接口*
这个是通过实现Parcelable接口，把要传的数据打包在里面，然后在接收端自己分解出来。这个是Android独有的，在其本身的源码中也用得很多，效率要比Serializable相对要好。
1、复写两个方法，分别是describeContents和writeToParcel
2、实例化静态内部对象CREATOR，实现接口Parcelable.Creator 。 以上这两步系统都已经帮我们自动做好了
3、自己写写我们所需要的构造方法，变量的get和set
        Intent putExtra(String name, Parcelable value)
      //接收参数
       intent.getParcelableExtra("key");
**对比**
android上应该尽量采用Parcelable，效率至上
编码上：
Serializable代码量少，写起来方便
Parcelable代码多一些
效率上：
Parcelable的速度比高十倍以上

serializable的迷人之处在于你只需要对某个类以及它的属性实现Serializable 接口即可。Serializable 接口是一种标识接口（marker interface），这意味着无需实现方法，Java便会对这个对象进行高效的序列化操作。  

 这种方法的缺点是使用了反射，序列化的过程较慢。这种机制会在序列化的时候创建许多的临时对象，容易触发垃圾回收。

Parcelable方式的实现原理是将一个完整的对象进行分解，而分解后的每一部分都是Intent所支持的数据类型，这样也就实现传递对象的功能了

---
###dp px sp的区别
* dp：就是dip(device independent pixels)设备独立像素，与密度无关的像素。一种基于屏幕密度的抽象单位。在每英寸160点(屏幕密度为160)的显示器上，1dp=1px；
* px：屏幕的实际像素。一般不用它作为单位，因为它会在不同的设备显示相同的效果。
* sp：与刻度无关的像素。主要用于定义字体的大小，而从来不再layout上使用。与dp相似，但是可以根据用户的字体大小首选项进行缩放，即sp除了与密度无关外，还与scale(缩放)无关。当屏幕密度为160时，1dp=1sp=1px；
---

###gravity和layout_gravity的区别

* android:gravity：view里面的内容在这个view中的位置
* android:layout_gravity：这个view相对于它父view的位置
**注意**
1.  对于horizontal的LinearLayout，把android:layout_gravity设为top、center、bottom、center_vertical才有意义；
2. 对于vertical 的LinearLayout，把android:layout_gravity设为left、center、right、center_horizontal才有意义；
3. RelativeLayout对android:layout_gravity不起作用
4. center已经包含了center_vertical和center_horizontal两种意义了，用的时候不要忘了
---
###margin和padding的区别
- margin是外边距
- padding是内边距

```
举个栗子：
一个LinearLayout中有一个ImageView，设置ImageView的padding和margin的属性，那么

padding指的是ImageView中图片距离图片框的距离
margin指的是整一个ImageView距离LinearLayout边界的距离
That's all. 
```
---

###weight的作用
* android:layout_weight
表明该控件可以在父控件中占据的“剩余”空间。默认的weight是0。﻿

---
###Handler机制
* Handler的定义:
   Handler主要用于接收子线程发送过来的数据, 并用此数据配合主线程进行UI的更新。   当应用程序启动时，[Android](http://lib.csdn.net/base/15)首先会开启一个主线程 (UI线程)，主线程主要为管理界面中的UI控件，进行事件的分发，好比如，你要点击一个 Button控件，Android就会通过此Buttond的监听器分发事件到此Button上，以此来响应你的操作。如果此时是一个需要耗时长的操作，例如：联网读取数据，或者读取本地较大的一个文件的时候，就不能把这些操作放在主线程当中了，如果被放在主线程中的话，界面会出现假死现象，如果5秒钟还没有完成的话，会收到Android系统的一个错误提示“强制关闭”。这个时候就需要把这些耗时的操作，放在一个子线程当中了，因为子线程可能会涉及到UI的更新，当新线程中有涉及到操作UI的操作时，就会对主线程产生危险，因此，Android提供了Handler作为主线程和子线程的纽带。也就是说，更新UI只能在主线程当中进行更新，在子线程中操作是危险的。
   由于Handler是运行在主线程当中(UI线程中)，它与子线程主要是通过Message对象来传递数据，这个时候，Handler就承担着接收子线程传过来的(子线程用sedMessage()方法传递)Message对象(里面包含数据)，把这些消息放入主线程队列中，配合主线程进行更新UI。
   注意：Handler 对象初始化后，就默认与对它初始化的进程的消息队列绑定，因此可以利用Handler所包含的消息队列，制定一些操作的顺序。
* Handler的主要作用
1.传递Message，用于接收子线程发送过来的数据, 并用此数据配合主线程更新UI。
    在Android中，对于UI的操作通常需要放在主线程中进行操作。如果在子线程中有关于UI的操作，那么就需要把数据消息作为一个Message对象发送到消息队列中，然后，由Handler中的handlerMessge()方法处理传过来的数据信息，并操作UI。当然，Handler对象是在主线程中初始化的，它需要绑定在主线程的消息队列中。
    类[sendMessage](file:///D:/android/android-sdk-windows/docs/reference/android/os/Handler.html#sendMessage(android.os.Message))([Message](file:///D:/android/android-sdk-windows/docs/reference/android/os/Message.html) msg)方法实现发送消息的操作。在初始化Handler对象时重写的handleMessage()方法是用来来接收Messgae并进行相关操作的。
2.传递Runnable对象，用于通过Handler绑定的消息队列，安排不同操作的执行顺序。
    Handler对象在进行初始化的时候，会默认的自动绑定消息队列。利用类post方法，可以将Runnable对象发送到消息队列中，按照队列的机制按顺序执行不同的Runnable对象中的run方法。
---
###什么的ANR, 如何避免
**ANR的定义**：在Android上，如果你的应用程序有一段时间响应不够灵敏，系统会向用户显示一个对话框，这个对话框称作**应用程序无响应**（ANR：ApplicationNotResponding）对话框。用户可以选择让程序继续运行，但是，他们在使用你的应用程序时，并不希望每次都要处理这个对话框。因此，在程序里对响应性能的设计很重要，这样，系统不会显示ANR给用户。

 **如何避免：**
* UI线程尽量只做跟UI相关的工作
* 耗时的操作(比如数据库操作，I/O，连接网络或者别的有可能阻塞UI线程的操作)把它放在单独的线程处理
* 尽量用Handler来处理UIThread和别的Thread之间的交互
* BroadcastReceiver要执行耗时操作时应启动一个service，将耗时操作交给service来完成

** ANR排错一般有三种类型：**
KeyDispatchTimeout(5 seconds) --主要是类型按键或触摸事件在特定时间内无响应
BroadcastTimeout(10 seconds) --BroadcastReceiver在特定时间内无法处理完成
ServiceTimeout(20 secends) --小概率事件 Service在特定的时间内无法处理完成

---
###显式意图和隐式意图区别,隐式意图的使用
* 一、显示调用Intent
```
Intent intent=new Intent(this,SecondActivity.class);
startActivity(intent);
```
* 二、隐式启动Intent
```
Intent intent=new Intent("com.xu.mytest");
startActivity(intent);
<activity android:name=".SecondActivity"> 
     <intent-filter> 
           <action android:name="com.xu.mytest"/> 
           <category android:name="android.intent.category.DEFAULT"/>
     </intent-filter>
</activity>
```
我们在这里给Activity设置了一个IntentFilter，但是值得注意的是，一个组件可以有多个IntentFilter，在过滤的时候只要有一个符合要求的，就会被视为过滤通过。
那我们就看看是怎样过滤的吧,首先我们应该明白一个大的思路：当我们隐式的启动一个组件的时候，就会一个一个的去过滤对应组件的全部，（比如你是隐式的启动一个Activity，就会一个一个的在全部Activity中筛选），然后根据Intent的所设置的action、category、data去比较IntentFilter所设置的这三个属性，相同的话就过滤留下来了。


* **区别**
** 显式启动**：直接指定要跳转的Activity类名，不用过滤，效率高，适用于同一个应用中的不同Activity跳转
** 隐式启动**：需要过滤，相对耗时，但可以找到所有之匹配的应用。适用于不同应用之间的Activity跳转。

---
###广播几种接收方式, 广播有几种类型, 区别
* #####接收方式
注册广播的方式一般有两种，在代码中注册称为动态注册；在AndroidManifest.xml中注册称为静态注册。
*** 动态注册：***
定义一个类继承自BroadcastReceiver，并复写父类的onReceive()方法，在activity中实例化自定义广播，使用Context的**registerReceiver(BroadcastReceiver, IntentFilter, String, Handler)**方法注册广播
**需要注意的是:**动态注册广播接收器一定都要取消注册。在onDestroy()方法中调用**unregisterReceiver()**方法就可以实现取消注册了。
**静态注册：**
* 首先新建一个BootCompleteReceiver类继承BroadcastReceiver

```
public class BootCompleteReceiver extends BroadcastReceiver { 
 @Override
     public void onReceive(Context context, Intent intent) { 
      Toast.makeText(context,"Boot Complete",Toast.LENGTH_LONG).show(); 
     }
}
```
* 接下来需要在AndroidManifest.xml声明BootCompleteReceiver这个类，BroadcastReceiver是安卓的四大组件之一，所以以下代码需要写在<application>标签内
```
<receiver android:name=".BootCompleteReceiver"> 
        <intent-filter> 
               <action android:name="android.intent.action.BOOT_COMPLETED"/> 
         </intent-filter>
</receiver>
```
这样就可以实现广播的静态注册了。
** 区别：**
第一种不是常驻型广播，也就是说广播跟随程序的生命周期。
第二种是常驻型，也就是说当应用程序关闭后，如果有信息广播来，程序也会被系统调用自动运行。

* #####广播的类型
**1.标准广播**标准广播是一种完全异步执行的广播，在广播发出之后，所有的广播接收器几乎会同时接收到这条广播消息。此类广播效率较高而且不能截断。
```
通过mContext.sendBroadcast(Intent)
或mContext.sendBroadcast(Intent, String)
发送的是无序广播(后者加了权限)；
```
![](http://upload-images.jianshu.io/upload_images/2314135-f4e397ebbf5e2fcb.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**2.有序广播**有序广播是一种同步执行的广播，广播发出之后，优先级高的广播接收器就可以先接收到广播消息，执行完该广播接收器的逻辑后，可以选择截断正在传递的广播或者继续传递，如果广播消息被截断，之后的广播接收器则无法收到广播消息。
```
通过mContext.sendOrderedBroadcast(Intent, String, BroadCastReceiver, Handler, int, String, Bundle)
发送的是有序广播。
//第一个参数：intent 
//第二个参数：String类型的接收者权限 
//第三个参数：BroadcastReceiver 指定的接收者 
//第四个参数：Handler scheduler 
//第五个参数：int 此次广播的标记  
//第六个参数：String 初始数据 
//第七个参数：Bundle 往Intent中添加的额外数据
<!-- 优先级相等的话，写在前面的receiver的优先级大于后面的 -->
<receiver android:name=".MyReceiver1" > 
        <!-- 定义广播的优先级 --> 
    <intent-filter android:priority="1000"> 
            <!-- 动作设置为发送的广播动作 --> 
            <action android:name="com.example.broadcast"/> 
    </intent-filter>
</receiver>
```
![](http://upload-images.jianshu.io/upload_images/2314135-eb2a70372c3fb0b2.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
[**参考**](http://www.jianshu.com/p/ea5e233d9f43)
* **区别**：
无序广播：所有的接收者都会接收事件，不可以被拦截，不可以被修改。
有序广播：按照优先级，一级一级的向下传递，接收者可以修改广播数据，也可以终止广播事件。

---

###开启Service的几种方式, 区别, Service和Activity之间如何传递数据
***开启Service的两种方式***：
* 1. **startService（Intent serviceIntent）** 一个组件可以通过startService的方式来开启Service服务。这种方式开启的Service可以调用**stopSelf（）**来停止服务，也可以通过在其他组件中调用stopService（）方法来停止。
* 2.**bindService（Intent service ,ServiceConnection conn ,Int flags）** 参数service是指要绑定的Service，conn是ServiceConnection对象，这个对象不能为null，flags为binding的类型，可以为0。 这种方式开启的Service会一直运行，直到没有组件绑定这个Service的时候系统才会停止Service。一般情况下，一个组件在不需要Service服务后要调用**unBindService（ServiceConnection conn）**来解绑Service。

**区别：**
* startService：生命周期与调用者不同，启动后若调用者未调用stopService而直接退出，Service仍会运行
* bindService：生命周期与调用者绑定（Service的生命周期依附于Context），调用者一旦全部退出，Service就会调用unBind->onDestroy
