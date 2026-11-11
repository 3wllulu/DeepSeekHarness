# DeepSeekHarness
零基础装好DeepSeek Harness
一、它是什么
DeepSeek Harness（命令叫 dsh）是 DeepSeek 官方开源的 AI 智能体工具。

和网页版最大的区别就一句：它不只是聊天，它能直接动你电脑上的文件。

DeepSeek 网页版	DeepSeek Harness
你给它的	一段文字	一个文件夹 + 一句话
它给你的	文字，你自己复制	直接改好你文件夹里的文件
能干什么	答疑、写文案	改代码、整理资料、批量处理文件
打个比方：模型是工人，很聪明但看不见你的电脑；Harness 就是把他放出来、递上工具的那一层。所以它本身不产生智能，它让模型能"动手"。

你只需要再记住两个词：

工作区：你授权给它操作的文件夹，它只能在这个范围里读写；
权限/审批：它要做有风险的操作（删文件、跑命令）时，会停下来问你"能干吗"。
二、先拿一个 API Key
dsh 只是外壳，真正干活的是模型，所以要给它一个凭证。

打开 DeepSeek，注册 / 登录；
左侧菜单点 API keys → 创建 API key；
名字随便填（比如 dsh），确定后立刻复制那串 sk- 开头的字符；
左侧菜单点 充值，充几块钱（按用量计费，试很久都够）；
把 Key 先存到记事本，下一步要用。
⚠️ 三点必须记住：

Key 只完整显示一次，关掉窗口就看不到，只能重新创建；
Key 等于你的钱包，不要贴到 GitHub、CSDN、群里或截图里；
怀疑泄露，立刻去平台删掉重建。
三、安装
方式一：桌面版（推荐，什么都不用装）
下载：打开官网 DeepSeek | 下载 DeepSeek，页面上方就是「DeepSeek Harness 全新桌面端」，按系统点按钮：

Windows → dsh-latest-windows-x64.exe
macOS（Apple 芯片 M1/M2/M3/M4） → dsh-latest-macos-arm64.dmg
认准 deepseek.com 域名。第三方打包的"汉化版"不要装。

Windows 安装：

双击 .exe；
若弹出"Windows 已保护你的电脑" → 点 更多信息 → 仍要运行（常规拦截，不是病毒）；
选择安装目录（默认即可；想换的话不能选磁盘根目录，且新文件夹要空的）；
等进度条走完，完成页直接点完成（默认勾了"立即启动"）。
macOS 安装：

双击 .dmg，把 App 拖进「应用程序」；
打开 App；若提示"无法验证开发者" → 系统设置 → 隐私与安全性 → 仍要打开。
安装包比较大（300 MB 起），因为 Node.js、Python 运行时都打包在内了，所以你电脑上不用提前装任何环境。

方式二：命令行版（Linux、Intel Mac 用这个）
要求 Node.js 24.9 以上（版本低了会直接报错）：

去 Node.js — Run JavaScript Everywhere 装 LTS 版，装完重新打开终端；
验证：node -v，应显示 v24.9.0 或更高；
进入你准备让它干活的文件夹：cd D:\dsh-test；
启动：
bash

npx @deepseek-ai/dsh web
AI代码解释
第一次会问 Ok to proceed? (y)，输入 y 回车。之后会自动打开浏览器，地址是 http://127.0.0.1:3080。

终端窗口不能关，关了服务就停了。想停止服务按 Ctrl + C。 下载慢可换镜像：npm config set registry https://registry.npmmirror.com

四、配置 Key，跑通第一句话
桌面版
第一次打开会弹出欢迎窗口，选择填写 API Key → 粘贴 → 保存并继续。

（如果你看到的版本左下角有"登录"入口，也可以直接登录 DeepSeek 账号用余额跑，效果一样；没有就用 Key。）

命令行版
浏览器 里点 设置 → 模型，粘贴 Key 保存。不用重启，立刻生效。

Key 是"只写不读"的，保存后只显示星号，存在 ~/.dsh/.credentials.yaml，不会上传。

然后选工作区（这步别漏）
不选工作区，输入框是灰的、打不了字——这不是 bug。

点 选择工作区，添加一个文件夹并选中。第一次建议新建个空目录专门测试，比如 D:\dsh-test，别一上来就选整个 C 盘。

试第一句话
把它丢进输入框、回车：

代码块

看一下当前工作区里有哪些文件，用一句话告诉我这个目录是干什么的
AI代码解释
你会看到它先"想一下"，然后调用工具（列目录、读文件），最后给结论。这就是它的全部工作方式。

💡 Windows 用户注意：点右上角 × 只是缩到托盘，任务还在后台跑。想真正退出：右键托盘图标 → 退出。

五、几个最容易遇到的问题
输入框是灰的？ → 没选工作区，见上面第四节。

npx 报 Node 版本错误？ → 装 Node 24+，装完重开终端。

3080 端口被占用？ → npx @deepseek-ai/dsh web --port 8080（--port 必须写在 web 后面）。

提示 401 / 认证失败 / MISSING_CREDENTIAL？ → Key 错了或没余额，去 设置 → 模型 重贴一次。

它说"路径在工作区之外"？ → 把那个目录加为工作区，不要去关安全限制。

它改坏了我的文件？ → 它不会自动备份，重要项目请先用 Git 提交。默认的 workspace-write 权限只让它改工作区里的文件，日常就用这个。

六、官方链接
下载页：DeepSeek | 下载 DeepSeek
开源仓库：https://github.com/deepseek-ai/deepseek-harness
官方文档：DeepSeek Harness
申请 Key：DeepSeek
dsh 处于开发者预览阶段，更新较快，界面上个别文案可能与你看到的不同，以官方文档为准。

标签
#deepseekharness
#AI智能体
#大模型
#教程
————————————————
版权声明：本文为CSDN博主「wllulu_」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/wllulu_/article/details/170457612
