# aidl-vs-provider

实操记录，并比较aidl和provider的区别。


aidl的server提供端

（1）也就是自己的主工程，在main目录下，新建一个aidl文件夹，
里面再新建一个，和MainActivity所在的最终目录地址，一样包名的文件夹，里面再新建一个aidl文件。

（2）在aidl文件里面，相当于是一个接口，可以定义各种暴露在外面方法，到时候client就是调用这些方法。

（3）需要make project一下，在build的classes里面生成对应的class文件。

（4）新建一个service文件，在里面通过Binder的对象关联好aidl文件，并实现aidl里面的方法，
方法里面可以调用主工程的任何方法，达到某种效果，或者返回内容。

（5）在清单文件，要声明好service，并定好action的值。


aidl的client使用（接收）端

（1）把aidl
的server提供端，在main目录下的整个aidl文件夹，移到自己的main目录下面。

（2）需要make project一下，在build的classes里面生成对应的class文件。

（3）通过bindService的方式，指定setAction和setPackage的值，然后通过ServiceConnection拿到aidl的对象，
通过对象就能使用aidl的方法。


provider端

（1）定义好DbOpenHelper的各种表。

（2）通过Provider继承ContentProvider，然后实现增删改查的方法，里面再关联好数据库的增删改查。

（3）定义好authorities的值，以及外部访问的uri的值，在内部定义好UriMatcher，可以判断是处理哪个数据库的表。

（4）这步可以不做，也可以做，塞入一些数据，方便后面接受者进行测试。

resolver端

（1）可以有，也可以没有，有对应的model类，便于数据库的值取出来的时候赋值。

（2）getContentResolver()通过uri进行增删改查，通过ContentValues来传值赋值。
