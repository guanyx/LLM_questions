# Hermes Agent对象拆解：Provider路由层详解第1张封面图文生图脚本

Create a dense technical cover infographic for social media in hand-drawn analytical style on pure white background. The theme is "Hermes Provider 路由层详解".

**Design Concept:**
不要用比喻，不要用吉祥物，也不要用工业机器。画面要尽量贴着对象本身。把 Provider Router 画成一个运行时对象边界：输入是什么，内部字段怎么分区，输出是什么，都要直接可见。整体感觉更像一张“对象解剖图 + 协议接口板 + 运行时档案页”。读者一眼就能看懂：什么东西进来，中间解了什么，最后吐出了什么样的稳定运行时结果。

**Layout Structure:**

**Top Section (Title Area - 20%):**

- Main title in bold, large font: "Hermes Provider 路由层详解"
- Small lead sentence under title: "这层不只是选模型。它把 provider 输入，解成可执行的运行时结果。"
- Add one small side note near the title:
  - "对象拆解 / Provider Routing / 01"
- 标题区要像一页技术档案封面，干净，克制，不花

**Central Section (Hero Object Anatomy - 75%):**
Create one dominant central routing object with annotated inputs, internal structure, and outputs:

- Place one large central object panel labeled "Provider Router"
  - 不要画成普通架构框图
  - 不要画成真实机器
  - 它应该像一个运行时对象的解剖视图
  - 用分层面板、字段分组、接口边缘和内部隔断来组织

- Left side: input surface
  - 在左侧放 5 张不同的 provider 输入卡片：
    - OpenAI-compatible
    - Anthropic
    - OpenRouter
    - 自定义 Endpoint
    - 内部 Gateway
  - each input card should carry compact incoming fragments:
    - 别名
    - 模型名
    - base_url
    - 认证方式
    - /v1
    - /responses
    - /anthropic
    - 401
    - 429
    - 402
  - 这些输入要明显异构，但不要故意画乱
  - 要让人看出来：进入同一个对象边界的，是一组彼此不对齐的运行时事实

- In the center object, split the anatomy into 4 internal zones:

  - Zone 1:
    - label: "Provider Identity / 身份归一"
    - role note:
      - "先把名字归一"
    - tiny field labels:
      - 别名归一
      - 家族映射
      - 规范名

  - Zone 2:
    - label: "ProviderDef / 静态定义"
    - role note:
      - "再把静态定义补齐"
    - visual form:
      - 这个区块内部用叠层结构表示
    - tiny field labels:
      - 元数据
      - overlay
      - 用户配置

  - Zone 3:
    - label: "Runtime Provider / 运行时绑定"
    - role note:
      - "这次到底怎么连"
    - 这个区块的视觉权重要比其他区块更重
    - tiny field labels:
      - base_url
      - api_key
      - 凭证池
      - 认证方式
      - API 模式

  - Zone 4:
    - label: "Recovery Policy / 恢复策略"
    - role note:
      - "出错以后先怎么救"
    - tiny field labels:
      - 刷新凭证
      - 轮转 key
      - fallback
      - 回主线路

- Show one explicit assembly path through the object:
  - 输入 provider 线索
  - 身份归一
  - 定义补齐
  - 运行时绑定
  - 恢复策略挂载
  - 输出运行时对象

- Right side: output surface
  - 从中央对象里输出一张干净的最终结果卡：
    - "已解析的 runtime provider"
  - 在结果卡下面放紧凑输出字段：
    - 规范 provider
    - 目标 endpoint
    - 已绑定凭证
    - API 模式
    - 已挂载恢复策略
  - 再把这个结果连到一个整齐的上层运行时条带：
    - Agent Loop
    - Tool System
    - Gateway
    - Cron
    - ACP
  - 右侧要有稳定、可执行、已定型的感觉

- Add 3 compact callouts around the center object:
  - "输入进来的不是同一种事实"
  - "中间处理的不是转发，是解析和绑定"
  - "出去的不是字符串，是运行时对象"

- Add one hard judgment line near the bottom of the central object:
  - "路由层的价值，不是多接几个模型，是把请求接成一个能运行的对象。"

**Key Visual Elements:**

- 中间只有一个主对象面板
- 左侧是异构输入卡片
- 中间拆出 4 个对象区块和字段级标签
- 右侧给出一个明确的已解析运行时对象
- 说明文字尽量围绕解析、绑定、执行来写
- 整张图要贴着真实运行时抽象，不要飞出去

**Visual Style:**

- 手绘分析图风格
- 更像对象解剖页，不像工业比喻图
- 更像运行时档案页，不像 PPT 架构图
- 内部标签要密，但构图要干净
- 多用分区、字段分组、接口边缘、引线和轻微辅助线
- 不要机器隐喻，不要卡通隐喻，不要吉祥物，不要装饰性伪 3D 物体
- 58% 中央对象拆解，17% 标签，25% 留白

**Color Palette:**

- 纯白背景
- 深海军蓝 (#2C3E50) 用于轮廓、文字和主分区
- 亮蓝 (#3498DB) 用于输入输出流向和关键接口线
- 低饱和绿 (#16A085) 用于已解析输出和稳定运行时交接
- 橙色 (#E67E22) 用于恢复相关标签和错误碎片
- 浅灰用于辅助线和次级标签

**Typography:**

- 所有主要标注都用简体中文
- 只有这些必要术语保留英文：Provider Router、ProviderDef、runtime provider、API mode、Agent Loop、Tool System、Gateway、Cron、ACP
- 标题要直接，要硬
- 小标签要像字段名和运行时备注
- 不要口号腔，不要虚词

**Overall Feel:**

- 硬一点，结构感强一点
- 尽量贴近真实软件对象
- 少比喻，多对象解剖
- 要让读者感觉自己在看一个核心抽象被摊开后的样子
- 第一眼最好就能感觉到："这一层本身就是个对象，不只是个判断分支"

Style: Dense technical analytical cover infographic, central runtime object anatomy of Provider Router, heterogeneous provider inputs on the left, resolved runtime object output on the right, field-level annotations, pure white background
