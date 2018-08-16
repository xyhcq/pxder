# pixiv downloader
目前只试做了一个下载某一画师的所有插画的功能，其余功能仍在开发中

简单写下说明（针对 Windows 用户）


## 准备
首先你需要先安装 Node.js  
[官网](https://nodejs.org) => 下载右边的“最新发布版” => 安装一路确定


## 安装
打开“命令提示符”或者“Powershell”，执行（后续命令皆为在此执行）
```bash
npm i -g pxder
```


## 配置
### 登录
```bash
pxder --login
```
然后会让你输入用户名密码，登录成功一次后以后如果没有错误则无需再次登录

如果要登出
```bash
pxder --logout
```

### 设置
这些配置可以通过追加`-S`或`--save`参数来永久保存以及覆盖，保存之后会直接结束程序  
不加则仅对本次执行有效
```bash
# 必须
-P 或 --path		<插画下载目录>

# 可选
-T 或 --thread 		<下载线程数>	# 默认为 5
-A 或 --auto-rename	# 当画师昵称改变时自动重命名下载文件夹（默认不开启）
--disable-auto-rename	# 取消上面的这个设定
```

例如，你在首次执行时可以运行这样的命令来设置  
**下载目录**为`D:\pixiv`，**下载线程数**为`6`，并且开启**自动重命名功能**
```bash
pxder -S -P "D:\pixiv" -T 6 -A
# 或
pxder --save --path "D:\pixiv" --thread 6 --auto-rename
```

如果要清除所有设置（恢复到初始状态），执行
```bash
pxder --clear
```
此举会将你的**登录状态**一并**清除**


## 正式使用
运行机制：
- 会将同一画师的作品下载在`(UID)画师名`格式的文件夹内，图片命名格式为`(PID)作品名`
- 文件（夹）名均会过滤掉所有 Windows 和 Linux 中不能或不推荐做文件名的符号
- 不存在的文件夹路径会被递归地自动创建
- 动图下下来会是所有帧的压缩包
- 下载时会忽略掉已经下载的插画，但是如果你下载到一半退出，会在`temp`文件夹内残留未下载完整的坏图片，你可以自行删除，或者当你再次开始同一画师的下载时也会删除
- 无需担心画师名字变动
- 下载超时时间为`30`秒，超时或网络错误会自动重试
- 小知识：在命令行中按下`Ctrl + C`可终止执行

### 下载某画师的所有插画作品（支持动图）
使用`--uid`参数，后跟画师的 UID，多个用英文半角逗号隔开
```bash
pxder --uid uid1,uid2,uid3,...
```

例如
```bash
pxder --uid 5899479,724607,11597411
```

## TODO
- [ ] 使用代理下载的选项
- [ ] 下载所有已关注画师的插画
- [ ] 智能增量下载
