---

### 🚀 Arch Linux 包管理速查表 · 
| 场景 | 命令（含常用别名） | 备注 / 小贴士 |
|---|---|---|
| **🗂️ 同步仓库** | `sudo pacman -Sy` | 仅更新索引，**不**升级系统 |
| | `sudo pacman -Syu` | 完整升级系统（含同步索引） |
| | `sudo pacman -Syyu` | 强制刷新索引再升级（解决仓库切换） |
| **📦 安装** | `sudo pacman -S 包名` | 支持正则：`pacman -S --needed firefox` |
| | `yay -S 包名` | AUR + 官方仓库混合安装 |
| | `yay -S --noconfirm 包名` | 无交互，CI 场景 |
| **🔍 搜索** | `pacman -Ss 关键字` | 搜索官方仓库 |
| | `yay -Ss 关键字` | 同时搜官方 + AUR，结果高亮 |
| | `pacman -Qs 关键字` | 搜索**已安装**包 |
| | `yay -Qs 关键字` | 同上，支持 AUR |
| **📋 信息** | `pacman -Qi 包名` | 已安装包的详情 |
| | `pacman -Si 包名` | 仓库包的详情 |
| | `yay -Qi 包名` | AUR 包也能看 |
| | `pactree 包名` | 依赖树（需 `pacman-contrib`） |
| **🧹 清理** | `sudo pacman -Sc` | 删除 `/var/cache/pacman/pkg` 旧版本 |
| | `sudo pacman -Scc` | **全部**清空缓存，慎用 |
| | `yay -Sc` | 同步清理官方 + AUR 缓存 |
| | `yay -Yc` | 删除**孤立**的 AUR 依赖 |
| **❌ 卸载** | `sudo pacman -R 包名` | 保留配置 |
| | `sudo pacman -Rs 包名` | 递归卸载，连带孤儿依赖 |
| | `sudo pacman -Rns 包名` | 再加 `--nosave`，**连配置一起删** |
| **🔧 数据库维护** | `sudo pacman -Dk` | 检查本地数据库一致性 |
| | `sudo pacman -Fy` | 更新文件索引 |
| | `pacman -F 文件名` | 查文件属于哪个包（需先 `-Fy`） |
| **🌟 AUR 专用** | `yay -Y --gendb` | 生成 AUR 开发包数据库 |
| | `yay -Y --devel --upgrade` | 升级所有 `-git` 开发版 |
| | `yay -Ps` | 打印系统统计（仓库数、包数、缓存大小） |
| | `yay -G 包名` | 仅下载 AUR 源码到当前目录 |
| **🔄 降级** | `sudo downgrade 包名` | 需安装 `downgrade`（AUR） |
| | `sudo pacman -U /var/cache/pacman/pkg/xxx.pkg.tar.zst` | 手动安装本地缓存旧版本 |
| **🆘 急救** | `sudo pacman -S $(pacman -Qnq)` | 重装所有包（修复误删系统文件） |
| | `sudo pacstrap /mnt base linux linux-firmware` | LiveCD 环境重建系统 |

---

### 🎨 终端配色提示
把下面追加到 `~/.bashrc` 或 `~/.zshrc`，即可让 `pacman` 与 `yay` 输出更漂亮：

```bash
# Pacman 彩色输出
export PACMAN_COLORS="ILoveCandy"

# Yay 彩色输出
export YAY_COLORS=1
```

---

### 🚀 一行安装「常用工具箱」
```bash
yay -S --needed base-devel git wget curl neovim exa bat fd ripgrep downgrade pacman-contrib
```

---

### 📌 别名速记（可选）
```bash
alias update='yay -Syu --devel --timeupdate'
alias cleanup='yay -Sc && yay -Yc'
alias orphans='sudo pacman -Rns $(pacman -Qtdq)'
```

---

祝使用愉快，滚挂随缘 😉
