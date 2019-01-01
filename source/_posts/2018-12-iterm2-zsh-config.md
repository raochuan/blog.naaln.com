---
title: 配置 iterm2
categories:
  - 技术 
date: 2018-12-27 16:14:59
tags:
---

## 安装 ZSH

```
	brew install zsh 
```

## 安装 oh-my-zsh

```
	sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

## 安装 oh-my-zsh 插件

#### `zsh-autosuggestions` 自动补全插件

```
	git clone git://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
```

编辑.zshrc文件

```
	plugins=(git zsh-autosuggestions)
```

#### `zsh-syntax-highlighting` 高亮

```
	brew install zsh-syntax-highlighting
```

#### `zsh-autosuggestions` 建议

```
	brew install zsh-autosuggestions
```

#### 我在用的插件

```
plugins=(
  git
  node
  npm
  sublime
  ruby
  sudo
  python
  osx
  pyenv
  gem
  python
  xcode
  github
  pip
  zsh-autosuggestions
  zsh-syntax-highlighting
)
```