[ubuntu使用github](https://blog.csdn.net/tina_ttl/article/details/51326684)

用户名就是邮箱地址
其中登录密码是指token
[github登录token获取](https://blog.csdn.net/m0_37844072/article/details/122715958)



# 提交更改
```linux
git add *
git commit -m "注释信息"
```

# push
```linux
//将本地代码与github连接起来
git remote add origin https://github.com/goushenngli/Road.git
//将修改推送到远程服务器，origin通常是指默认远程服务器
git push origin master
```