---
title: 如何通过配置密钥来实现 SSH 免密登录？
date: 2024-04-21 22:08:04
categories:
    - Tutorials
    - OpsConfig
tags:  
    - SSH
    - Login
cover: https://ooo.0x0.ooo/2024/04/21/OpnhsM.jpg
---

# Configure SSH Key for Password-free Login



## Base

SSH 客户端通过基于加密通讯的协议（Secure Shell Protocol），登录远程机器上并开启远程终端会话

> 关于 SSH 的更多细节请查阅手册： `man -s 1 ssh `

- SSH 命令的常用字段

```bash
ssh [user@]host [-p port]
```



## Generate SSH Key Pair

SSH 使用**非对称**加密算法生成**密钥对**，包括公钥和私钥。

> SSH 支持的非对称加密算法包括：
>
> - **RSA（Rivest-Shamir-Adleman）**：基于大素数的质因数分解问题，最常见的公钥加密算法之一。
> - **DSA（Digital Signature Algorithm）**：数字签名算法，适用于签名和验证，但不适用于加密数据。
> - **ECDSA（Elliptic Curve Digital Signature Algorithm）**：基于椭圆曲线的数字签名算法，拥有比 RSA 和 DSA 更高的安全性和更小的密钥尺寸。
> - **Ed25519**：基于椭圆曲线的数字签名算法，具有高性能和高安全性，同时提供了较短的密钥长度。
> - **Curve25519**：基于椭圆曲线的密钥交换算法，用于生成密钥交换所需的公钥和私钥。

使用 `ssh-keygen` 来生成密钥对：

```bash
ssh-keygen [-t dsa | ecdsa | ecdsa-sk | ed25519 | ed25519-sk | rsa]
```

如果 OS 是 Windows，生成的密钥对会存储在 `C:\Users\username\.ssh` 目录下，带`.pub` 后缀的文件是公钥文件



## Copy Public Key to Remote Machine

在非对称密码体制中，通过**公钥**加密，**私钥**解密,

因此你需要在把之前生成的密钥对里面的**公钥**，发送到远程机器上。

### Command: scp

首先通用的是 `scp` 命令，

> `scp` fomat: `scp source ... target`
>
> 其中 `source` 和 `target` 可以被指定为
>
> - 本地路径，如：`~/folder/filename`
> - 远程主机（可提供 path），如：`[user]@host:[path]`
> - URL，如：`scp://[user]@host[:port][/path]`

先用 `scp` 把公钥文件复制到远程机器上:

```bash
scp ./ssh_key.pub user@host:/home/user/.ssh
```

然后在远程机器上，用 `cat` 配合标准输出把公钥文件追加到 `~/.ssh/authorized_keys` 中:

```bash
cat ~/.ssh/ssh_key.pub >> ~/.ssh/authorized_keys
```

注意请使用 `>>` 而非 `>` 来执行流重定向，以把公钥文件追加至 `authorized_keys` 中，而不是覆盖 `authorized_keys` 中的内容。

### Command: ssh-copy-id

其次，如果是在 linux 本地机器上发送到远程机器，可以选择 `ssh-copy-id` 命令,

> ssh-copy-id format: `ssh-copy-id [-i [identity_file]] [user@]host`
>
> 其中 `identity_file` 可以被指定为公钥文件

只需要简单一条命令（准确来说是一段 script）：

```bash
ssh-copy-id -i ./ssh_key.pub user@host
```

然后公钥文件就会被自动地追加到远程机器的 `~/.ssh/authorizedkeys` 文件里面了



## Login via SSH without using a password

完成了上面两个步骤之后就能通过 SSH 无需密码口令地开启远程机器上的会话了