项目路径：E:\\project\\QTcreate\\3Login
***
### 注意：
- 3.2中对于`#ifndef`的理解，参考[百度百科](https://baike.baidu.com/item/%23ifndef/2835043)
 条件指示符`#ifndef`的最主要目的是防止一个源文件两次包含同一个头文件。
```C++
语句 1 #ifndef 标识1

语句 2 #define 标识1

语句 3 #endif

语句 4 ……

语句 5 ……

//该段代码意思是：如果标识1没有被定义，则重定义标识1，即执行语句2、语句3;如果标识1已经被定义，则直接跳过语句2、语句3，直接执行语句4、语句5、……
```
- 3.2中对于第13行代码`Q_OBJECT`，`Q_OBJECT`是Qt定义的宏，其中包含了Qt最重要的一个机制，即信号和槽。但凡是[[Qt头文件QObject]]类，必须在第一行代码写上`Q_OBJECT`，无论是否使用(只有继承了`QObject类`的类，才具有信号槽的能力)。
- 3.2中16行`~LoginDialog();`是指[[析构函数]]，它会在每次删除所创建的对象时执行，析构函数有助于在跳出程序（比如关闭文件、释放内存等）前释放资源。
- (错误)%%3.2中16行`~`指二进制取反，参考[菜鸟教程](https://www.runoob.com/cplusplus/cpp-operators.h%%tml)%%
- 3.2中第二段代码第8行中继承了QDialog，LoginDialog(QWidget \*parent) 类比看，父类QDialog的构造函数也需要参数
***
# 参考链接
[学习链接](https://dengjin.blog.csdn.net/article/details/115082243):https://dengjin.blog.csdn.net/article/details/115082243

***
***
***
# 代码
	logindialog.h
```C++
#ifndef LOGINDIALOG_H
#define LOGINDIALOG_H

#include <QDialog>
//在下面只是定义了这些类对象的指针，并不需要该类完整的定义
class QLabel;
class QLineEdit;
class QPushButton;


class LoginDialog : public QDialog
{
    //但凡是Qt头文件QObject类，必须在第一行代码写上`Q_OBJECT`，无论是否使用(只有继承了`QObject类`的类，才具有信号槽的能力)。
    Q_OBJECT
public:
    // explicit：explicit关键字防止隐式类型转换，创建构造函数,构造函数的函数名和类名一致
    explicit LoginDialog(QWidget* parent = 0);

    //~LoginDialog()：类的析构函数，和类名一致，不过前面加个波浪号(~)
    ~LoginDialog();

//槽函数
private slots:
    void login();

private:
    QLabel *userLabel;
    QLabel *pwdLabel;

    QLineEdit *userEditLine;
    QLineEdit *pwdEditLine;

    QPushButton *loginBtn;
    QPushButton *exitBtn;

};
#endif // LOGINDIALOG_H
```
	logindialog.cpp
```C++
#include "logindialog.h"

#include <QLabel>
#include <QLineEdit.h>
#include <QPushButton>
#include <QMessageBox>

LoginDialog::LoginDialog(QWidget* parent) :QDialog(parent)
{
	//为什么new的时候要添加this
	userLabel = new QLabel(this);
	userLabel->move(70, 80);
	userLabel->setText(tr("用户名"));

	//用户名输入框
	userEditLine = new QLineEdit(this);
	userEditLine->move(140, 80);
	userEditLine->setPlaceholderText(tr("请输入用户名"));

	//
	pwdLabel = new QLabel(this);
	pwdLabel->move(70, 130);
	pwdLabel->setText(tr("密码"));

	//
	pwdEditLine = new QLineEdit(this);
	pwdEditLine->move(140, 130);
	pwdEditLine->setPlaceholderText(tr("请输入密码"));

	loginBtn = new QPushButton(this);
	loginBtn->move(50, 200);
	loginBtn->setText(QString("登录"));

	exitBtn = new QPushButton(this);
	exitBtn->move(210, 200);
	exitBtn->setText(tr("退出"));

	//信号与槽关联
	connect(loginBtn, &QPushButton::clicked, this, &LoginDialog::login);
	connect(exitBtn, &QPushButton::clicked, this, &LoginDialog::close);
}
void LoginDialog::login()
{
	//判断用户名和密码是否正确
	if (userEditLine->text().trimmed() == QString("tom") && pwdEditLine->text() == tr("123456"))
	{
		accept();
	}
	else
	{
		QMessageBox::warning(this, tr("警告"), tr(""), QMessageBox::Yes);
	}
	userEditLine->clear();
	pwdEditLine->clear();
	userEditLine->setFocus();
}

LoginDialog::~LoginDialog()
{

}

```