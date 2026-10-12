# webnovel-writing

中文网络小说创作全流程工程化 Skill。覆盖从选题、扫榜、拆对标、大纲、细纲、正文日更、去AI味到审校的完整链路，支持长篇（起点/番茄/晋江/七猫）与短篇（知乎盐言/豆瓣阅读/七猫短篇）。

## 功能特性

- **全流程覆盖**：扫榜选材 → 拆对标书 → 搭大纲/细纲 → 写正文 → 去AI味 → 审校
- **双体裁支持**：长篇连载（10万字+）与短篇（8k-2万字）
- **30+题材模板**：玄幻、仙侠、都市、古言、现言、悬疑、甜宠、复仇、快穿、系统流、末世、宫斗、年代、双男主等
- **14个自动化脚本**：AI句式检测、退化扫描、标点归一化、字数统计、状态追踪、大纲视图等
- **去AI味引擎**：多Gate分级检测，从轻度到重度分级处理
- **审校体系**：按平台（番茄/起点/知乎盐言）定制评分标准
- **已有作品导入**：把已发表章节反向工程为可续写工程

## 目录结构

```
webnovel-writing/
├── SKILL.md                          # 主入口与场景路由
├── LICENSE
├── references/                       # 方法论知识库（按需加载）
│   ├── long-scan/                    # 长篇扫榜选题
│   ├── long-analyze/                 # 长篇拆对标书
│   ├── long-write/                   # 长篇写作（大纲/正文/日更/大修）
│   │   └── genre-prose-cards/        # 30+题材 prose 卡片
│   ├── short-scan/                   # 短篇市场数据
│   ├── short-analyze/                # 短篇拆解
│   ├── short-write/                  # 短篇写作
│   │   └── genre-styles/             # 10大短篇题材风格
│   ├── deslop/                       # 去AI味
│   ├── review/                       # 审校
│   │   └── rubrics/                  # 平台评分标准
│   ├── import/                       # 已有作品导入
│   └── cover/                        # 封面风格参考
└── scripts/                          # 可执行工具脚本
    ├── check-ai-patterns.js          # AI句式检测
    ├── check-degeneration.js         # 模型退化扫描
    ├── check-delivery-contract.js    # 交付契约检查
    ├── check-outline-contract.js     # 大纲契约检查
    ├── normalize-punctuation.js      # 标点归一化
    ├── wordcount_core.py             # 字数统计
    ├── outline_view.py               # 大纲视图
    ├── storyctl.py                   # 故事控制
    ├── author_memory_commit.py       # 作者记忆提交
    ├── tracking_commit.py            # 状态追踪提交
    └── ...
```

## 脚本使用

### 前置要求

- Node.js >= 16（用于 .js 脚本）
- Python >= 3.8（用于 .py 脚本）

### AI 句式检测

```bash
node scripts/check-ai-patterns.js --check --fail-on=blocking 正文文件.md
```

检测 AI 味句式（破折号滥用、否定排比、旁白总结等），blocking 级别必须修改。

### 模型退化扫描

```bash
node scripts/check-degeneration.js --check 正文文件.md
```

检测复读、截断、工程词泄漏等退化信号。

### 标点归一化

```bash
# 标准模式
node scripts/normalize-punctuation.js 正文文件.md

# 知乎盐言模式（保留「」）
node scripts/normalize-punctuation.js --quote-mode yan 正文文件.md
```

### 字数统计

```bash
python scripts/wordcount_core.py 正文文件.md
```

### 大纲视图

```bash
python scripts/outline_view.py --unit {单元ID} 卷纲文件.md
```

## 核心设计理念

1. **先定情绪，再定故事**：每个场景必须服务一个明确目标情绪
2. **从验证过的模式出发**：扫榜找方向，拆文找模块，对标找节奏
3. **模块组装**：把对标书的角色看成功能位，用自己的素材填充
4. **AI味主要问题不是语法**：是过度圆滑、工整、解释充分——改写目标是增加口语、停顿和具体动作

## 共享文件说明

以下文件在多个场景目录中存在副本（内容完全一致），这是为了让每个场景目录自包含：
- `anti-ai-writing.md` — 去AI味写作指南
- `author-memory.md` — 作者记忆系统
- `banned-words.md` — 禁用词表
- `style-resolution.md` — 风格决策
- `tracking-initialization.md` / `tracking-transaction.md` — 状态追踪

后续版本计划将这些抽到 `references/common/` 目录。

## License

[MIT](./LICENSE)
