使用github issues的方式搭建博客，思路真的很好 [教程](https://blog.meekdai.com/post/Gmeek-kuai-su-shang-shou.html)
但是过程中也遇到了两个问题，记录下

## 已有xxx.github.io

但是我搭建过程中首先碰到的就是，我已经有个 [xxx.github.io](http://xxx.github.io/) 的仓库了，怎么办？

好在作者给了方案。 **创建一个仓库名称为blog。这样你就可以通过 [xxx.github.io/blog](http://xxx.github.io/blog) 来访问**

这里细说一下，先按照教程去建立仓库。之后要在pages 选项里面勾选github actions

<img width="862" alt="image" src="https://github.com/user-attachments/assets/ad7700e3-7645-4826-b0ff-7dd2890c90a8">

之后新建带标签的issues后，主页才会有[xxx.github.io/blog](http://xxx.github.io/blog) 链接，此时才能访问

##  绑定域名

此时去cf绑定域名，会发现[xxx.github.io/blog](http://xxx.github.io/blog) 这个地址cname解析不了，折腾了半天

其实只用放 [xxx.github.io](http://xxx.github.io/) 解析，然后用你的**blog.xxx.com**去访问，就能直接打开了

