## 思路：

- 先把图片全部放到一个 QList 里，存放地址或者 QIcon 都可以。  
- 设置一个 int 标签 Flag ＝ 0 (QList 第一个的索引是 0) ，当前为第几个图片，Flag 就是几。  
- 点上一张的响应是 Flag--，下一张就是 Flag++。然后共同调用放图片的函数：  
	- 判断 Flag >= 0 && Flag <QList.size ()  
	- 加载 QList [Flag] 对应的图片  
[参考:百度知道](https://zhidao.baidu.com/question/1432022528359803179.html)

## 代码部分
代码主要参考的是：[CSDN博客](https://blog.csdn.net/qq_42214953/article/details/105295186)
### solu.h
```C++
#ifndef SOLU_H
#define SOLU_H
# include<QDir>
#endif // SOLU_H
#include<qdebug.h>
#include<QFileInfoList>
#include<qstring.h>
QString load ="/home/erdan/my_Desktop/data/安全帽/data-helmat/JPEGImages/";
QFileInfoList FindFile(QString name)
{
    //检查路径是否存在
    QDir dir(name);
    if(!dir.exists())
    {
        qDebug()<<"文件夹不存在"<<Qt::endl;
    }
    
    //取到所有的文件和文件名，去掉.和..文件夹
    dir.setFilter(QDir::Dirs | QDir::Files | QDir::NoDotAndDotDot);
    dir.setSorting(QDir::DirsFirst);
    //将其转化为一个list
    QFileInfoList list = dir.entryInfoList();
    if(list.size()<1)
        qDebug()<<"文件夹为空"<<Qt::endl;
    return list;
}
```

### mainwindow.cpp
```C++
#include "mainwindow.h"
#include "ui_mainwindow.h"
#include<qpixmap.h>
#include<solu.h>
# include<qdir.h>
# include<QMessageBox>
#include<QString>
#include<qfiledialog.h>
static QFileInfoList list = FindFile(load);
static int  photoIndex=0;//查看照片的索引，为List的下标
static char newphotoIndex = '0';//用于命名新添加的照片
MainWindow::MainWindow(QWidget *parent) :
    QMainWindow(parent),
    ui(new Ui::MainWindow)
{
    ui->setupUi(this);
    //设置
    this->setMaximumSize(500,800);
    this->setMinimumSize(400,500);
}
MainWindow::~MainWindow()
{
    delete ui;
}
//照片显示
void MainWindow::DisplayPhoto(QString name)
{
    QPixmap photo(load+name);
    photo = photo.scaled(ui->label->width(),ui->label->height(),Qt::KeepAspectRatio);
    ui->label->setPixmap(photo);
}
//下一张
void MainWindow::on_pushButton_3_clicked()
{
   if(list.size()<1)
    {
       QMessageBox::warning(this,QStringLiteral("error"),QStringLiteral("暂无照片"));
       return;
    }
   DisplayPhoto(list.at(photoIndex).fileName());
   ++photoIndex;
   if(photoIndex>=list.size())
   {
       photoIndex=0;
   }
}
//上一张
void MainWindow::on_pushButton_4_clicked()
{
    if(list.size()<1)
     {
        QMessageBox::warning(this,QStringLiteral("error"),QStringLiteral("暂无照片"));
        return;
     }
    DisplayPhoto(list.at(photoIndex).fileName());
    --photoIndex;
    if(photoIndex<0)
    {
        photoIndex=list.size()-1;
    }
}
//添加照片
void MainWindow::on_pushButton_2_clicked()
{
    //打开文件窗口选择文件
    QFileDialog *fileDialog = new QFileDialog(this);
    fileDialog->setGeometry(100,100,800,900);
    fileDialog->setDirectory(".");
    //过滤文件
    fileDialog->setNameFilter("Image Files(*.jpg *.jpeg *.png *.gif)");
    //设置可以选择多个文件
    fileDialog->setFileMode(QFileDialog::ExistingFiles);
    fileDialog->setVisible(true);
    //得到选择文件名
    QStringList fileName;
    if(fileDialog->exec()==QDialog::Accepted)
    {
        fileName=fileDialog->selectedFiles();
        for(int i =0;i<fileName.size();++i)
        {
            //将选择的文件拷贝进load中
            qDebug()<<fileName.at(i);
            qDebug()<<load;
            QString name = fileName.at(i);
            //对照片类型进行判断
            QString newName;
            if(name.right(4)==".jpg")
            {
                newName =load+newphotoIndex+".jpg";
            }
            if(name.right(4)==".png")
            {
                newName =load+newphotoIndex+".png";
            }
            if(name.right(4)==".gif")
            {
                newName =load+newphotoIndex+".gif";
            }
            qDebug()<<newName;
            if(!QFile::copy(fileName.at(i),newName))
            {
            QMessageBox::warning(this,QStringLiteral("error"),QStringLiteral("添加失败"));
                return;
            }
              QMessageBox::warning(this,QStringLiteral("error"),QStringLiteral("添加成功"));
              newphotoIndex++;
              //更新list
              list = FindFile(load);
              //显示新添加的照片
              DisplayPhoto(list.at(list.size()-1).fileName());
        }
    }
}
void MainWindow::on_pushButton_clicked()
{
    QString deleteName = load+list.at(photoIndex).fileName();
    if(QFile::remove(deleteName))
    {
        QMessageBox::warning(this,QStringLiteral("error"),QStringLiteral("删除完成"));
    }
   //更新
    photoIndex=0;
    list =FindFile(load);
    DisplayPhoto(list.at(photoIndex).fileName());
}
```


# 参考链接
[实际使用代码](https://blog.csdn.net/qq_42214953/article/details/105295186)
[其他参考](https://www.cnblogs.com/craigtao/p/6640470.html)