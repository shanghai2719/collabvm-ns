# README – CollabVM 服务器 Windows 安装与使用指南

**管理员支持：**  
👉 https://t.me/Nulltestfun1

---

## 📦 1. 下载 ZIP 文件并解压  
1. 点击 **Download ZIP**（或从发送者获取文件）  
2. 下载完成后 → **右键 → 解压到当前文件夹**  
3. 打开解压后的文件夹  

### 如果无法解压  
- Windows 10/11：右键 → 解压全部  
- Windows 7/8：建议安装 **7-Zip**（免费）

---

## 🖥 2. 系统要求  
CollabVM Server 支持以下系统：

| 系统 | 支持 | 备注 |
|-----|------|------|
| **Windows 7** | ✔ | x32 / x64 均可 |
| **Windows 8 / 8.1** | ✔ | x32 / x64 |
| **Windows 10** | ✔ | x32 / x64 |
| **Windows 11** | ✔ | x32 / x64 |
| Windows XP / Vista | ❌ | 不保证可用 |

> 建议使用 Windows 10/11 x64，性能更好。

---

## ⚙ 3. 在 Windows 安装 QEMU  
CollabVM 使用 QEMU 运行虚拟机。

### 🔗 QEMU Windows 下载地址  
- **QEMU x32:** https://qemu.weilnetz.de/w32/  
- **QEMU x64:** https://qemu.weilnetz.de/w64/

### 📝 安装步骤
1. 下载与你系统对应的 QEMU（32 位或 64 位）  
2. 运行安装程序 → Next → Install  
   - 安装视频：  
     📹 https://flopa2.qzz.io/img/qemu.mp4  
3. 将 QEMU 添加到系统 PATH（用于在 CMD 中运行）  
   - 视频教程：  
     📹 https://flopa2.qzz.io/img/qemu-in.mp4

---

## 💾 4. 创建虚拟硬盘 (Disk Image)
1. 打开存放 ISO 与虚拟机文件的文件夹  
2. 在文件夹地址栏输入：
   ```
   cmd
   ```
   按 Enter 打开 CMD  
3. 输入以下命令创建硬盘文件：

### RAW 格式
```
qemu-img create -f raw mydisk.img 20G
```

### QCOW2 格式
```
qemu-img create -f qcow2 mydisk.img 20G
```

> `20G` 为虚拟硬盘容量，可随意调整。

---

## 🚀 5. 启动 CollabVM Server  
1. 打开解压后的文件夹  
2. 在地址栏输入：
   ```
   cmd
   ```
3. 输入启动命令：

```
nt-collab.exe {端口} {文件夹}
```

示例：
```
nt-collab.exe 80 http
```
或
```
nt-collab.exe 6044 http
```

### 防火墙提示  
→ 点击 **允许访问（Allow Access）**

### 如果 CMD 显示：
```
Collab VM Server started
```
表示服务器启动成功。

---

## 🌐 6. 开放端口 & 使用自定义域名

### A) 本地访问  
```
http://localhost:{端口}
```

例如：
```
http://localhost:6044
```

### B) 外网访问（需要开放端口）
需要：

#### 1. 路由器 Port Forwarding  
开放你运行的端口（如 80、6044）

#### 2. Windows 防火墙放行端口  
添加 Inbound Rule → Port → Allow

#### 3. 自定义域名  
在域名管理后台添加 A 记录 → 指向公网 IP  
```
yourdomain.com → 123.45.67.89
yourdomain.com:{端口}
```

---

## 🌍 7. 使用 NGROK（无需端口映射）
1. 下载： https://ngrok.com/download  
2. 登录后运行：
   ```
   ngrok http {端口}
   ```

示例：
```
ngrok http 6044
```

3. Ngrok 会生成访问链接：
```
https://xxxxx.ngrok-free.app
```

---

## 🛠 8. 进入管理面板 / 创建虚拟机

### 打开管理页面  
```
http://localhost:{端口}/admin/config.html
```
或
```
https://你的域名/admin/config.html
```

**默认密码：**
```
collabvm
```

---

## 🖥 创建虚拟机（New VM 设置参考）

- **Auto Start：** ✔  
- **URL Name：** ns  
- **Display Name：** win10  

### VNC 设置  
- Address：`127.0.0.1`  
- Port：`5900` (必须 ≥5900)

### QMP 设置  
- Socket Type：Local / TCP  
- Address：自定义  
- Port：`5800`  

### Guacamole 参数  
```
Max Attempts: 5
```

### Hypervisor  
```
QEMU
```

### 启动命令示例
```
qemu-system-x86_64 -hda win10.img -m 4G -boot d -cdrom Win10.iso
```

### Snapshot  
- Off  
或  
- Hard Drive Snapshots

### Turns （轮流模式）  
- ✔ Enabled  
- Turn Time：20 秒

### Votes  
- ✔ Enabled  
- Vote Time：60 秒  
- Cooldown：60 秒

### Agent  
- ✔ Agent Enabled  
- ✔ Use Virtio（若系统安装了驱动）

### Uploads  
- ✔ Enabled  
- Cooldown：30 秒  
- Max File Size：`20971520`  
- Max Filename Length：100

完成后 → 保存 → 回主页检查虚拟机是否运行。

---

## 🎉 完成  
需要以下服务可联系我：  
- 定制 `.exe`  
- 自动化脚本  
- QEMU 最佳配置  
- CollabVM Web 前端 UI 重构  
- 远程协助部署  

管理员支持：  
👉 https://t.me/Nulltestfun1
