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

（4）在清单文件，要声明好provider，并定好authorities的值。

（5）这步可以不做，也可以做，塞入一些数据，方便后面接受者进行测试。


resolver端

（1）可以有，也可以没有，有对应的model类，便于数据库的值取出来的时候赋值。

（2）getContentResolver()通过uri进行增删改查，通过ContentValues来传值赋值。


通过上面的记录，可以很直观看见，

（1）aidl配合性，相比起来比provider麻烦，如果server端，修改aidl文件，
server端要重新make project一下，然后再把aidl文件复制到client端，然后client端要重新make project一下。

（2）aidl灵活性，相比起来比provider灵活，provider只能操作数据库，其他一些方法无法通过getContentResolver()获取调用，
而aidl无论数据库，还是一些方法都能调用，想定义什么方法都行。


进程间通信，aidl和provider最后总结，

（1）简单的业务，而且只需要操作数据库就能满足需求的，就推荐使用provider，非常方便。

（2）复杂的业务，方法种类繁多的，或者是硬件类即时性获取传输的，就推荐使用aidl，也很方便。

aidl和provider两个的例子demo，都有，但是由于上传的文件限制是25m以内，所以就上传重要的一些文件，工程你们自己建。
