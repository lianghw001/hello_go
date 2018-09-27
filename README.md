# 安装 go 语言开发环境


## 1.安装编辑器
如果有图形界面,建议安装VScode
我没有使用图形界面，因此只安装vim

```$ sudo yum install vim```

简单vim教程

* i → Insert 模式，按 ESC 回到 Normal 模式
* :wq → 保存并退出
* :help显示帮助

## 2.安装、配置golang
### 安装

```$ sudo yum install golang```
### 创建工作空间

```$ mkdir $HOME/gowork```
### 配置环境变量
* 打开当前用户根目录

````cd $HOME ````
* 查看当前目录所有文件

````ls -a````
* 使用vim编辑(若没有则创建) .profile文件

````vim .profile````

* 编辑 .profile为

````
export GOPATH=$HOME/gowork
export PATH=$PATH:$GOPATH/bin
````

* 在.bashrc文件中添加(也是使用vim操作)

````source ~/.profile````

* 重启

````sudo reboot````



## 3.试运行
### 创建源代码目录(其中github-user改为自己的GitHub用户名)

````$ mkdir $GOPATH/src/github.com/github-user/hello -p````

### 使用 vim 创建 hello.go

````
package main

import "fmt"

func main() {
    fmt.Printf("hello, world\n")
}
````
### 运行
````$ go run hello.go````


## 4.将.go文件编译并运行

（文件夹命名错误，环境变量未配置好，都可能导致这一步出现error）

````
$ go install github.com/github-user/hello
$ hello
````




[Git日常使用总结](https://gitee.com/lianghwsysu/course_note_mad/blob/master/%E8%AF%BE%E7%A8%8B%E7%AC%94%E8%AE%B0/Git%E6%97%A5%E5%B8%B8%E4%BD%BF%E7%94%A8%E6%80%BB%E7%BB%93.md)
