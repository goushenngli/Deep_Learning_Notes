# 步骤
1. 在VS里面将程序变成Release版本[![vHs2Ks.png](https://s1.ax1x.com/2022/09/07/vHs2Ks.png)](https://imgse.com/i/vHs2Ks)
2. 编译一下，会生成一个.exe程序
3. 在项目目录下找到这个.exe程序，在项目目录下的x64/Release/目录下[![vHs724.png](https://s1.ax1x.com/2022/09/07/vHs724.png)](https://imgse.com/i/vHs724)
4. 复制文件到新目录下
5. 在目录的地址栏输入cmd进入命令行格式
6. 输入windeployqt  \*.exe(\*是指文件名)，点击回车
7. 如果提示找不到windeployqt命令，则将Qt程序的bin目录添加到环境变量Path下，再重启电脑使环境生效[![vH6nTx.png](https://s1.ax1x.com/2022/09/07/vH6nTx.png)](https://imgse.com/i/vH6nTx)
8. 可以看到桌面的文件夹多了很多文件[![vHysdx.png](https://s1.ax1x.com/2022/09/07/vHysdx.png)](https://imgse.com/i/vHysdx)
9. 下载打包软件[EnigmaVirtualBox_v9.70](https://enigmaprotector.com/assets/files/enigmavb.exe)
10. 设置软件语言为中文并重启程序[![vHyWSe.png](https://s1.ax1x.com/2022/09/07/vHyWSe.png)](https://imgse.com/i/vHyWSe)
11. 选择主程序，点击浏览，选择主程序，点击打开[![vH631e.png](https://s1.ax1x.com/2022/09/07/vH631e.png)](https://imgse.com/i/vH631e)
12. 选择添加，添加文件夹递归[![vH6t0I.png](https://s1.ax1x.com/2022/09/07/vH6t0I.png)](https://imgse.com/i/vH6t0I)
13. 选择.exe文件所在文件夹，点击确定，点击确定![[Pasted image 20220907143806.png]][![vH6g7q.png](https://s1.ax1x.com/2022/09/07/vH6g7q.png)](https://imgse.com/i/vH6g7q)
14. 点击文件选项，勾选压缩文件，点击确定[![vH653F.png](https://s1.ax1x.com/2022/09/07/vH653F.png)](https://imgse.com/i/vH653F)
15. 点击执行封包，等待运行结束，结束后点击关闭，关闭软件，在原始的.exe文件夹下会出现另一个.exe文件，新出现的这个程序就是有动态编译库的文件，可以不依赖环境运行[![vH6bH1.png](https://s1.ax1x.com/2022/09/07/vH6bH1.png)](https://imgse.com/i/vH6bH1)[![vH6X4K.png](https://s1.ax1x.com/2022/09/07/vH6X4K.png)](https://imgse.com/i/vH6X4K)
<br>
# 主要参考：
[CSDN](https://blog.csdn.net/weixin_45013621/article/details/123442111)
<br>
[CSDN修改图标](https://blog.csdn.net/Eric_ZN88/article/details/106937946)