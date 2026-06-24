# Typora Windows 激活工具

由于`obsidian`不能像`typora`那样随时随地的打开`markdown`文件，下载网上别人破解工具我又怕ta留后门，所以就学习了这篇 [52破解论坛](https://www.52pojie.cn/forum.php?mod=viewthread\&tid=2084047)的文章，将最新版破解了一下。目前破解方法只限于`windows`。

现在用了两周，暂时没发现有啥bug。

## 影响版本

- **主要支持**: Typora 1.13.7 (Windows)
- 其他版本可能兼容，但仅 1.13.7 经过验证。运行时会自动检测版本并提示。

## 安装包信息

| 项目         | 信息                                                                 |
| ---------- | ------------------------------------------------------------------ |
| **文件名**    | `typora-setup-x64.exe`                                             |
| **版本**     | 1.13.7.0                                                           |
| **大小**     | \~93.7 MB                                                          |
| **公司**     | typora.io                                                          |
| **描述**     | Typora Setup (Inno Setup)                                          |
| **SHA256** | `04dc5d0ec1ddae9ab1d405be578c2d486e48cca9295029f79d532db80032ab40` |

***

## 方法一：脚本注入激活（永久）

通过解压 asar、修改 Electron Fuse、注入 Hook 代码实现永久激活。

### 依赖安装【需管理员权限】

```bash
npm install asar @electron/fuses
```

需要 Node.js 环境（建议 v16+）。

### 运行

```bash
# 自动查找 Typora（从注册表搜索）
node crack.js

# 或手动指定 Typora 路径
node crack.js "D:\software\Typora"
node crack.js "D:\software\Typora\Typora.exe"
```

### 激活

脚本执行完毕后 Typora 会自动启动。在激活窗口输入以下格式的激活码：

```
+XXXXXXXX#
```

- 以 `+` 开头，`#` 结尾
- 中间为任意字符，例如: `+12345678#`

### 运行日志

正常执行输出如下：

```
未自动找到 Typora，请手动输入路径。
支持: 安装目录 (D:/software/Typora) 或 exe 路径
路径: C:\Program Files\Typora
Typora 路径: C:/Program Files/Typora
=== 初始化 ===
Typora.exe → .bak
app.asar → .bak
asar → app/
app/ → app.bak/
app.asar 已删除
Fuse 已修改
Typora 版本: 1.13.7
Hook 注入完成

====================================
  激活码格式: +XXXXXXXX#
  示例: +12345678#
  必须以 + 开头、# 结尾，中间任意字符
====================================

Typora 已启动。
```

### 激活效果

![激活页面](img/1.png)

![激活成功](img/2.png)

### 注意事项

- 运行前请确保 Typora 进程已完全关闭，否则会报 `EBUSY` 错误
- 脚本会自动备份原始文件（`.bak` 后缀），如需还原可手动恢复

***

## 方法二：重置试用期（无限试用）

直接双击运行 `reset_typora.bat`，或右键选择"以管理员身份运行"。

该脚本会做两件事：

1. 删除注册表 `HKEY_CURRENT_USER\Software\Typora` 下的激活信息
2. 删除 `%AppData%\Typora\profile.data` 配置文件

重新打开 Typora 即恢复 15 天试用。到期后重复运行即可。
