---
title: Hexo Blog Develop Notes
date: 2024-04-15 21:56:31
categories:
  - Tutorials
  - BlogDev
tags:
  - Hexo
  - NVM
  - Post
lang: en
cover: https://ooo.0x0.ooo/2024/04/16/Om8pOa.png
---
# Hexo Blog Develop Notes



## Prerequisites: nvm for npm & node

Hexo also need git, but just one command:

```bash
sudo apt install git
```



### Why nvm?

Until now, my ubuntu machine are using node version `18.20.2` and npm version `10.5.2`.

Hexo sometimes need a higher version number of both npm and node, then you may need **nvm**.

nvm is a version manager for Node.js, it allows you to quickly install and use different versions of node via the command line.

> Git Repo for nvm is [here](https://github.com/nvm-sh/nvm?tab=readme-ov-file#usage).



### Install nvm

Recommanded install nvm using bash：

```BASH
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.2/install.sh | bash
```

Then add nvm to the `Path`:

```bash
# ~/.bashrc or some kind of ~/.zshrc
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/bin/nvm.sh" ] && . "$NVM_DIR/bin/nvm.sh"  # This loads nvm
alias nvm='. ~/.nvm/nvm.sh'
```

 Check nvm version by:

```bash
nvm --version
```



### Usage

#### check node version

To check the node version:

```bash
nvm ls
```

#### install specific version of node

To install a specific version of node:

```bash
nvm install ${NODE_VERSION_NUMBER}
```

> If you just wan to install the latest release of node, just `nvm install node`

When you install a new node version, it would change your node version into it.

If you want to change node into a specific version of node: 

```bash
nvm use ${NODE_VERSION_NUMBER}
```

Remove a specific version of node:

```bash
nvm uninstall ${NODE_VERSION_NUMBER}
```

#### install npm for each node

nvm also alow you install different version of npm for each node:

```bash
nvm install-npm ${NPM_VERSION_NUMBER} ${NODE_VERSION_NUMBER}
```





## First Step: Install & Init & Config & Generate hexo

Source doc: [hexo doc](https://hexo.io/docs/)



### Install

Recommand using global instal hexo-cli for beginner:

```
npm install -g hexo-cli
```

After that, you can check you hexo version:

```bash
hexo -v
```

and get such output:

```bash
INFO  Validating config
hexo: 7.1.1
hexo-cli: 4.3.1
os: linux 5.4.0-144-generic Ubuntu 20.04.6 LTS (Focal Fossa)
node: 18.20.2
acorn: 8.10.0
ada: 2.7.6
ares: 1.27.0
base64: 0.5.2
brotli: 1.0.9
cjs_module_lexer: 1.2.2
cldr: 44.1
icu: 74.2
llhttp: 6.1.1
modules: 108
napi: 9
nghttp2: 1.57.0
nghttp3: 0.7.0
ngtcp2: 0.8.1
openssl: 3.0.13+quic
simdutf: 4.0.8
tz: 2024a
undici: 5.28.4
unicode: 15.1
uv: 1.44.2
uvwasi: 0.0.19
v8: 10.2.154.26-node.36
zlib: 1.3.0.1-motley
```



### Init

One command: `hexo init`, but remember run `npm install`

```bash
hexo init ${FOLDER_NAME}
cd ${FOLDER_NAME}
npm install
```



### Config

A just-init hexo blog folder would seem like:

```
.
├── .github
|   ├── dependabot.yml
├── node_modules
|   ├── ...
|   └── ...
├── scaffolds
|   ├── draft.md
|   ├── page.md
|   └── post.md
├── source
|   └── _posts
|       └── hello-world.md
├── themes
|   └── .gitkeep
├── _config_landscape.yml
├── _config.yml
├── .gitignore
├── package-lock.json
└── package.json
```

In `_config.yml`:



 

### Generate

```bash
hexo gen
```



```bash
hexo clean
```



## Second Step: deploy it on GitHub page

For update and deploy the hexo blog in one step:

```bash
hexo clean && hexo generate && hexo deploy
```

or 

```bash
hexo clean && hexo generate && hexo server
```

But if you deploy firstly, you need to configure the `_config.yml`:

```yml
# Deployment
# Docs: https://hexo.io/docs/one-command-deployment
deploy:
  type: git
  repo: https://github.com/<username>/<username>.github.io.git
  branch: main
```

Then run:

```bash
hexo deploy
```



## Last Step: Change your theme

I use this theme: [hexo-theme-butterfly](https://butterfly.js.org/)

Config theme: [butterfly](https://butterfly.js.org/posts/21cfbf15/)





## Afterword: How to writting a blog post?

Source: [hexo writting](https://hexo.io/docs/writing)

