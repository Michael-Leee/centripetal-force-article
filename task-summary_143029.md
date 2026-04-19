# 向心力 PDF 字体修复

## 问题
用户反馈 PDF 没有文字。根本原因：ctex 包的 `fontset=mac` 在 macOS 15 Sequoia 上无法找到 macOS 系统字体（STSong/STHeiti），导致中文无法渲染。

## 解决方案
使用 TeX Live 2025 自带的 **Fandol 中文字体**，通过 `fontspec + xeCJK` 显式指定字体文件路径：

```latex
\setCJKmainfont{FandolSong-Regular.otf}[
  Path=/usr/local/texlive/2025/texmf-dist/fonts/opentype/public/fandol/
]
```

## 修复内容
- 移除 ctex bundle（mac fontset 在 macOS 15 上失效）
- 使用 `ifxetex` + `fontspec` + `xeCJK` 组合
- 显式指定 Fandol.otf 完整路径（TeX Live 内置，无需额外安装）
- 修复 fbox 双括号语法错误

## 验证
- PDF 大小：144KB（之前 135KB，无中文）
- CJK 字节：3530（中文内容丰富）
- Fandol 字体已嵌入 PDF 流中

## GitHub
已推送 commit 71ff738 到 main 分支。
