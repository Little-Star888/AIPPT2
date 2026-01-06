# AIPPT - AI PPT 生成工作流

从文章内容生成精美 PPT 的完整工作流。

## 工作流

```
文章内容 → ASCII PPT 框架 → AI 生图 → 完整 PPT
```

## 使用方法

### 第一步：文章转 ASCII PPT 框架

给文章内容，Claude 会生成 ASCII 布局框架：

```
帮我把这篇文章生成 ASCII PPT 框架
```

### 第二步：选择风格生成图片

选择风格（哆啦A梦/火影忍者/赛博朋克等），逐页生成：

```
用哆啦A梦风格生成 PPT 第 2 页
```

## 支持的风格

| 类别 | 风格 |
|-----|------|
| 基础 | 扁平插画、等距视图、科技渐变、线条图标 |
| 动漫 | 哆啦A梦、火影忍者、吉卜力、新海诚、海贼王 |
| 潮流 | 赛博朋克、蒸汽波、像素艺术、涂鸦街头 |
| 艺术 | 水墨国风、梵高星空、装饰艺术 |
| 3D/材质 | 皮克斯3D、乐高积木、黏土动画 |
| 漫画 | 漫威漫画 |

## 文件说明

```
AIPPT/
├── SKILL.md                    # 主入口，工作流指引
├── README.md                   # 本文件
├── skills-ascii-ppt.md         # 完整示例
└── tips/
    └── 文章转ascii-ppt方法论.md  # 详细方法论
```

## API 配置

生图使用 Gemini Image API，需配置 API Key：

1. 访问 [ismaque.org/register](https://ismaque.org/register?aff=npk7)
2. 获取 API Key
3. 调用时传入 Key
