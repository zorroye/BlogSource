---
title: grub2设置等待时间、设置修改密码
tags:
  - 鸟哥的私房菜
categories:
  - Linux
  - 鸟哥的私房菜
id: '209'
abbrlink: 4236291604
date: 2011-06-21 18:32:00
---

1、设置等待时间：10秒

> 修改 /etc/grub.d/30\_os-prober 里的一个数字  

> if keystatus; then  
>  if keystatus –shift; then  
>  set timeout=-1  
>  else  
>  set timeout=10 #把0改为10  
>  fi  
>  else  
>  if sleep$verbose –interruptible 3 ; then  
>  set timeout=0  
>  fi  
>  fi

> 保存后，运行 sudo update-grub

> 重启后自动进入grub2界面，不需要再按shift调出来

  

  

2、设置修改grub2时的密码

1\\ grub-mkpasswd-pbkdf2生成加密的密码

2\\ 向/etc/grub.d/00\_head末尾追加:

  
 cat << EOF

          set superusers="ywz"

          password\_pbkdf2   ywz    grub.pbkdf2.sha512.10000.\`\`\`\`\`              #即刚才运行命令时显示的代码

          EOF

  

  

  

参考：1、 [http://leonhongchina.blog.163.com/blog/static/1802941172011018450428/](http://leonhongchina.blog.163.com/blog/static/1802941172011018450428/)

2、[http://www.douban.com/note/64464787/](http://www.douban.com/note/64464787/)