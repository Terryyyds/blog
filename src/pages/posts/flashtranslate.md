---
layout: '../../layouts/MarkdownPost.astro'
title: 'FlashTranslate: Lightning-Fast AI Translation UI'
pubDate: 2025-11-27
description: 'React + Vite 框架下的跨平台翻译工具，支持 Claude / Gemini / GPT 系列一键切换与本地密钥管理。'
author: 'Terry'
cover:
    url: 'https://s2.loli.net/2025/11/28/OfbeRG7lZo8TV14.jpg'
    square: 'https://images.unsplash.com/photo-1504384308090-c894fdcc538d?auto=format&fit=crop&w=900&h=900&fit=crop&q=80'
    alt: 'Abstract interface with bright strokes suggesting speed and translation'
tags: ["Project", "AI", "Web", "Translation"]
theme: 'light'
featured: true
---
# FlashTranslate：让 AI 翻译回归「一键直达」

我用 React + TypeScript + Vite 做了一款轻量级的翻译 UI——FlashTranslate。它开箱即用、跨平台，支持 Claude、Gemini、GPT 三家模型自由切换，按一下回车就能完成检测与翻译。

你可以在 <a href="https://flashtranslate.terrylog.cn" target="_blank" rel="noopener noreferrer">flashtranslate.terrylog.cn</a> 体验这款工具。 

![FlashTranslate interface mock|inline](https://s2.loli.net/2025/11/28/OfbeRG7lZo8TV14.jpg)

![FlashTranslate interface|wide](https://s2.loli.net/2025/11/28/OfbeRG7lZo8TV14.jpg)

## ✨ 为什么做这个

- 想要一个纯前端、无需安装客户端的翻译入口，打开浏览器就能用。  
- 在多模型之间切换时不想频繁复制粘贴密钥和端点，希望设置留在本地。  
- 需要快速计数、检测语言、复制结果，减少写作/开发时的上下文切换。

## 🚀 核心特性

- **一键翻译**：自动检测源语言，支持 16+ 目标语言，按下 `Enter` 即可完成翻译。  
- **多模型切换**：内置 Claude 3.5 Haiku（系统密钥可直接用），也可改用 Gemini 2.5 Flash Lite 或 GPT-4o Mini，并支持自定义代理/端点。  
- **清晰的双栏布局**：原文/译文并排，展示字数统计、检测结果徽章、加载遮罩，以及一键复制译文。  
- **本地隐私优先**：密钥只存储在浏览器 `localStorage` 中，不会被上传；顶部状态徽章实时显示密钥校验状态。  
- **键盘/状态反馈**：输入回车触发翻译，顶部状态 pill 标记当前模型与密钥有效性。

![Game Animation|inline](https://s2.loli.net/2025/11/28/iX6vFug9fSrmHya.jpg)



## 🛠️ 技术栈与结构

- **React + TypeScript + Vite**：快速开发与构建体验。  
- **组件**：`LanguageSelector`、`TranslationArea`、`SettingsModal` 拆分 UI；`App.tsx` 管理翻译流程与状态。  
- **服务层**：`translationService.ts` 统一封装各家 API 调用与密钥校验；`constants.ts` 管理语言列表，`types.ts` 统一类型定义。  
- **样式**：Tailwind 通过 CDN 注入，减少本地配置成本。

## 📦 快速开始

```bash
git clone https://github.com/Terryyyds/flashtranslate
cd flashtranslate
npm install
npm run dev   # 默认 http://localhost:3000
```

## 🔧 模型与密钥管理

- 默认使用内置 Claude 端点与系统密钥：选择 Claude 时可将 API Key 留空即可体验。  
- 想使用自己的密钥？输入后会自动填充官方默认端点（Gemini `https://generativelanguage.googleapis.com`、OpenAI `https://api.openai.com/v1`、Claude `https://api.anthropic.com/v1`），也可以自行改为代理地址。  
- 密钥保存位置：`localStorage` 中的 `flash_translate_api_config`，点击齿轮图标进入设置并可一键清除。  
- 需要静态注入 Gemini 密钥时，可在构建前设置 `GEMINI_API_KEY` 环境变量。

## 🧭 使用方式

1. 选择目标语言（源语言自动检测）。  
2. 在 “Original Text” 输入或粘贴内容，按回车或点击 Translate。  
3. 查看检测语言与译文，点击复制图标即可复制结果。  
4. 顶部状态徽章会显示当前模型与密钥是否通过校验。

## 📂 查看源码

仓库地址：<a href="https://github.com/Terryyyds/flashtranslate" target="_blank" rel="noopener noreferrer">github.com/Terryyyds/flashtranslate</a>  
欢迎 issue / PR，一起把体验和多语言覆盖做得更好。

## 🔮 接下来可能做的事

- 增加批量翻译与文件导入（如 `.txt/.md`）入口。  
- 提供多段落并行翻译与用量提示。  
- 简单的历史记录 / 收藏句段，方便复用。  

## 🔗 联系我

- <a href="https://terrylog.cn" target="_blank" rel="noopener noreferrer">个人网站</a>  
- <a href="https://github.com/Terryyyds" target="_blank" rel="noopener noreferrer">GitHub</a>  
- <a href="http://linkedin.com/in/yu-deng-396901303" target="_blank" rel="noopener noreferrer">LinkedIn</a>
