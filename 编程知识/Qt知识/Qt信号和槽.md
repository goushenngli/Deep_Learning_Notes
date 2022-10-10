信号和槽是对象间的一种通信机制

# 相关知识介绍
## moc介绍
moc，即元对象编辑器，所做的工作就是对带有Q_OBJECT宏的类进行处理，生成对应的moc_xx x.cpp。
[![vxvAVU.png](https://s1.ax1x.com/2022/09/15/vxvAVU.png)](https://imgse.com/i/vxvAVU)
## 信号和槽绑定
```C++
//Qt5、6用法
connect(pA, &ClassA::SendSingal, pB, &ClassB::RecvSignal);

//Qt4的用法
//connect(pA, &ClassA::SendSingal, pB, &ClassB::RecvSignal);
```
# 信号和槽
其实信号和槽内部并没有实现什么，主要是提供一个标记，和C++的关键字进行区分，在moc工具处理的时候方便识别哪些是Qt内部的东西。
## signals:
Qt提供的，信号关键字，内部其实就是一个`public 空宏`，可以理解为就是一个`public`
```C++
define signals public
```
## slots:
Qt提供的，槽关键字，内部其实是一个空宏，连权限修饰符都没有
```C++
define slots
```

## Q_OBJECT
Qt的moc工具会先判断每个类里面有没有Q_OBJECT宏，如果有，就进行宏展开
```C++
/* qmake ignore Q_OBJECT */
#define Q_OBJECT \
public: \
    QT_WARNING_PUSH \
    Q_OBJECT_NO_OVERRIDE_WARNING \
    static const QMetaObject staticMetaObject; \
    virtual const QMetaObject *metaObject() const; \
    virtual void *qt_metacast(const char *); \
    virtual int qt_metacall(QMetaObject::Call, int, void **); \
    QT_TR_FUNCTIONS \
private: \
    Q_OBJECT_NO_ATTRIBUTES_WARNING \
    Q_DECL_HIDDEN_STATIC_METACALL static void qt_static_metacall(QObject *, QMetaObject::Call, int, void **); \
    QT_WARNING_POP \
    struct QPrivateSignal {}; \
    QT_ANNOTATE_CLASS(qt_qobject, "")
```
抛去Qt编译警告的一些宏后：
```C++
/* qmake ignore Q_OBJECT */
#define Q_OBJECT \
public: \
    static const QMetaObject staticMetaObject; \
    virtual const QMetaObject *metaObject() const; \
    virtual void *qt_metacast(const char *); \
    virtual int qt_metacall(QMetaObject::Call, int, void **); \
private: \
	Q_DECL_HIDDEN_STATIC_METACALL static void qt_static_metacall(QObject *, QMetaObject::Call, int, void **); \
    struct QPrivateSignal {}; \
    QT_ANNOTATE_CLASS(qt_qobject, "")
```
其中包含函数声明，函数定义就在moc生成的.cpp文件里面