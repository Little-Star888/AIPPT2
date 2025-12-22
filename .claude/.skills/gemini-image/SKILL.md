---
name: gemini-image
description: 当用户想要生成图片、画图、绘画、创建图像、AI作画时使用此 Skill。支持文生图和图生图。
---

# Gemini 图像生成

当用户表达画图意图时（如"画一个..."、"生成图片..."、"帮我创作..."），使用此 Skill。

## 调用步骤

### 1. 读取配置
- 读取 `config/secrets.md` 获取 API Key

### 2. 构造 prompt

| 模式 | prompt 格式 | 示例 |
|-----|------------|------|
| 文生图 | `描述文字` | `一只可爱的橘猫` |
| 图生图 | `图片URL 描述文字` | `https://xxx.jpg 画类似风格` |
| 多图参考 | `URL1 URL2 描述文字` | `https://a.jpg https://b.jpg 融合两张图` |

图生图需先上传图片，参考 `tips/image-upload.md`。

### 3. 调用 API

```bash
curl -s -X POST "https://api.apicore.ai/v1/images/generations" \
  -H "Authorization: Bearer API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "模型名称",
    "prompt": "提示词",
    "size": "尺寸比例",
    "n": 1
  }'
```

### 4. 返回结果

从响应中提取 `data[0].url` 返回给用户。

## 模型选择

| 模型 | 说明 |
|-----|------|
| `gemini-3-pro-image-preview` | 标准版（默认） |
| `gemini-3-pro-image-preview-2k` | 2K 高清 |
| `gemini-3-pro-image-preview-4k` | 4K 超清（用于高清化） |

## 调用注意事项（⚠️ 重要）

### curl JSON 格式要求

**❌ 错误写法（会导致解析失败）：**
```bash
-d '{
    "model": "xxx",
    "prompt": "中文描述",
    "size": "1024x576"
  }'
```

**✅ 正确写法：**
```bash
-d '{"model": "xxx", "prompt": "English description", "size": "1024x576", "n": 1}'
```

### 关键要点

1. **使用单行 JSON** - 去掉所有换行和缩进，避免 curl 解析错误
2. **prompt 使用英文** - 避免中文字符编码问题，API 更稳定处理英文
3. **中文内容处理** - 如需图片中显示中文，在 prompt 中用拼音或描述性英文替代
4. **错误信息识别** - 如果看到 `blank argument where content is expected` 说明 JSON 格式有问题

### 调试技巧

```bash
# 测试 API 连通性
curl -s -X POST "https://api.apicore.ai/v1/images/generations" \
  -H "Authorization: Bearer $API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"model": "gemini-3-pro-image-preview", "prompt": "a cat", "size": "1024x1024", "n": 1}'
```

## 参考文档

- `案例/案例展示.html` - 风格参考与 PPT 案例图库（15+ 种风格参考图，3 套完整 PPT 案例）
- `tips/文章转ascii-ppt方法论.md` - 将文章转换为 ASCII PPT 框架的完整方法论
- `tips/ppt生图方法论.md` - PPT 生图方法论与 Prompt 模板
- `tips/chinese-text.md` - 中文文字处理技巧
- `tips/4k-upscale.md` - 4K 高清化增强
