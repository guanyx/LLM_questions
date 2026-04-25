# 《Agent记忆系统怎么实现？》组图脚本

## 一、这组图的主线

这组图不准备再把 Agent 记忆系统讲成“短期记忆、长期记忆、情景记忆、语义记忆”这种偏概念化的知识卡片。

它真正要解决的是一个更稀缺的问题：

**如果今天真的要做一个 Agent 记忆系统，应该先搭什么、后搭什么、哪些模块最容易做错、不同实现路径的代价又是什么。**

所以这组图的叙事重点，不是“记忆这个词本身很重要”，而是让读者看见一条完整的工程链：

- 先定义要解决的问题
- 再拆记忆系统的分层
- 然后讲写入链路
- 再讲召回链路
- 接着讲存储分工
- 最后讲冲突、压缩、遗忘和落地顺序

这组图真正想建立的判断是：

**Agent 记忆系统不是一个向量库，也不是一份聊天记录，而是一条从写入、召回、压缩到治理的运行时链路。**

---

## 二、建议张数

建议做成 **8 张图**：

- 第 1 张：封面 / Agent 记忆系统不是一个库
- 第 2 张：先定义记忆系统到底要解决什么问题
- 第 3 张：真正能落地的记忆架构，通常至少四层
- 第 4 张：实现的第一重点，是写入链路
- 第 5 张：实现的第二重点，是召回链路
- 第 6 张：记忆到底该放哪里，不同存储怎么分工
- 第 7 张：最容易被低估的三个模块
- 第 8 张：如果现在就开工，最稳的落地顺序是什么

这个张数的优点是：

- 主线完整
- 每张图只讲一个判断
- 信息密度足够高，但不会把单张塞得过满
- 看完后，读者会形成一条清晰的实现路径，而不是只记住几个名词

---

## 三、统一视觉方向

### 1）整体风格

- 视觉气质：Tech Editorial / System Blueprint / Runtime Memory Anatomy
- 基调：白底、结构化、技术杂志式、信息密度高但秩序清楚
- 关键词：write path、recall path、storage split、compaction、forgetting、governance
- 禁止：大脑拟人化、发光神经元、科幻记忆宫殿、抽象云雾、悬浮芯片海报

### 2）封面核心隐喻

封面最值得利用的，不是“脑子”隐喻，而是：

**把记忆系统画成一条有入口、有分流、有存储、有召回、有压缩、有治理的工程总线。**

更具体地说：

- 左侧是信息流入
- 中间是写入分流和不同记忆层
- 右侧是召回、压缩和当前上下文窗口
- 底部或外围再挂上冲突处理、遗忘、评测、技能沉淀这些治理模块

让人一眼看出：

**这不是一个静态仓库，而是一套持续流动的系统。**

### 3）统一术语策略

- 描述文字尽量用中文
- 核心术语保留英文：
  - Working Set
  - Episodic Memory
  - Semantic Memory
  - Procedural Memory
  - Write Path
  - Recall Path
  - Compaction
  - Forgetting
  - Skills
- `Working Set` 强调当前工作面，不叫万能记忆
- `Write Path` 和 `Recall Path` 要在全组图中反复保持一致

### 4）配色建议

- 深蓝：系统边界、标题、主框体
- 亮蓝：主链路、信息流、写入和召回箭头
- 绿色：稳定事实、成功经验、已验证流程
- 橙色：风险、噪音、冲突、过期信息
- 灰色：注释、背景网格、次级说明

### 5）叙事规则

- 每张图只讲一个主要判断
- 每张图都要体现“信息如何流动”，而不是只摆静态方块
- 不讲空泛趋势口号，要落到对象、链路和边界
- 每张图底部都保留一句判断式金句

---

## 四、组图总主线

整组图的叙事顺序应该是：

**先把问题立住，再把架构拆开，然后顺着“写入 -> 召回 -> 存储 -> 治理 -> 落地顺序”一路往下推。**

如果压缩成一句导语，可以写：

**Agent 记忆系统真正难的，不是把历史存下来，而是决定什么该写、什么该取、什么该压、什么该忘。**

---

## 五、逐张分镜脚本

### 第 1 张：封面 / Agent 记忆系统不是一个库

**标题建议：**

Agent记忆系统怎么实现？

**副标题建议：**

它不是一个向量库，而是一条从写入、召回到治理的工程链路

**这一张承载的信息：**

- 这组图不是记忆概念科普
- 主题是“如何落地实现”
- 核心判断是记忆系统不是单一存储，而是一条运行时链路

**适合直接上图的一句话：**

真正的 Agent 记忆系统，不是把历史塞进一个库，而是让信息在正确的时间写进去、取出来、被压缩、被淘汰。

**画面结构建议：**

- 整张图做成一条横向工程总线
- 左侧是 `inputs`：
  - user messages
  - tool results
  - files
  - web content
  - errors
- 中间是 `Write Path` 分流区：
  - raw events
  - filter
  - routing
- 中部偏下分成四块存储层：
  - Working Set
  - Episodic Memory
  - Semantic Memory
  - Procedural Memory
- 右侧是 `Recall Path`：
  - task judge
  - retrieve
  - rerank
  - context pack
- 右上角是 `current context window`
- 底部外挂三个治理模块：
  - conflict resolution
  - compaction
  - forgetting

**视觉重点：**

- 不是一个大数据库圆柱
- 是一条可流动、可分流、可回收的系统链
- 封面一眼要看出“写入”和“召回”是两条不同路径

**底部金句：**

记忆系统的核心，不是存储，而是信息流动的秩序。

---

### 第 2 张：先定义记忆系统到底要解决什么问题

**标题建议：**

做记忆系统前，先别急着选库

**副标题建议：**

先回答你到底想解决连续性、长任务、经验沉淀，还是成本问题

**这一张承载的信息：**

- 记忆系统不是为了“显得高级”
- 真正需要解决的是四类工程问题
- 不先定义目标，后面所有选型都会发散

**适合直接上图的一句话：**

没有验收目标的记忆系统，最后往往只会变成一堆昂贵的历史数据。

**可直接上图的文案块：**

- 跨会话连续性：用户不用重复背景
- 长任务稳定性：任务拉长后不掉线
- 经验沉淀能力：同类问题第二次更快做对
- 成本可控：召回和重排不能把系统拖死

**画面结构建议：**

- 中间放一个大标题框：`Memory Goals`
- 周围放四个目标卡片：
  - continuity
  - long-horizon stability
  - experience reuse
  - cost control
- 每个目标卡片下放对应指标：
  - preference consistency
  - long task success rate
  - repeated error rate
  - prompt cost / latency
- 左下角做一个反例小块：
  - 只堆历史
  - 只做向量库
  - 只加上下文长度
- 用橙色标注“看起来很强，实际上无法验收”

**底部金句：**

先钉验收指标，再谈记忆架构，否则系统只会越做越虚。

---

### 第 3 张：真正能落地的记忆架构，通常至少四层

**标题建议：**

实用的 Agent 记忆系统，通常至少四层

**副标题建议：**

不是为了概念完整，而是因为不同信息根本不该放在同一层

**这一张承载的信息：**

- Working Set、事件层、事实层、过程层的分工不同
- 记忆失败往往不是“没存”，而是“存错层”
- 不同层决定不同写法、不同召回方式和不同生命周期

**适合直接上图的一句话：**

把所有信息都塞进同一层，最后你得到的不是记忆系统，而是一锅越来越脏的上下文。

**画面结构建议：**

- 做一个四层结构板，从近到远排列：
  - Working Set
  - Episodic Memory
  - Semantic Memory
  - Procedural Memory
- 每层保留三类标签：
  - 存什么
  - 什么时候用
  - 不该存什么
- 例如：
  - Working Set：最近消息、当前目标、临时状态
  - Episodic：工具调用、失败案例、历史结论
  - Semantic：用户偏好、项目约束、稳定事实
  - Procedural：技能、流程、最佳实践
- 每层旁边用不同颜色标出生命周期：
  - 短
  - 中
  - 长
  - 可复用

**视觉重点：**

- 要体现“距离当前上下文的远近”
- 不是知识分类表，而是运行时分工图

**底部金句：**

记忆分层的意义，不是学术命名，而是让不同信息进入正确的生命周期。

---

### 第 4 张：实现的第一重点，是写入链路

**标题建议：**

大多数记忆系统，先坏在写入链路

**副标题建议：**

问题往往不是取不出来，而是一开始就写错了东西

**这一张承载的信息：**

- 写入链路是实现的第一重点
- 原始事件不能直接等于长期记忆
- 重要性判断和分类路由决定系统会不会越积越脏

**适合直接上图的一句话：**

记忆系统最怕的不是忘，而是把不该记的东西记得太认真。

**主链路文案建议：**

`raw event -> importance check -> routing -> persist -> consolidation`

**画面结构建议：**

- 左侧放多个原始事件卡片：
  - user request
  - tool output
  - file change
  - error log
- 中间放 `importance gate`
  - cross-session value?
  - high reuse?
  - worth prompt space?
- 从 gate 分三条流：
  - 进入事件层
  - 进入事实层
  - 进入过程层
- 旁边加一个橙色反例框：
  - 临时状态被写成长期偏好
  - 一次性试错被固化成经验
- 右侧再补两个写入模式：
  - sync write
  - async consolidation

**要强调的判断：**

- 先记录 raw events
- 再判断是否值得长期保存
- 高价值信息同步写入
- 其余候选信息后台固化

**底部金句：**

写入链路决定记忆质量，后面的检索只是放大前面的选择。

---

### 第 5 张：实现的第二重点，是召回链路

**标题建议：**

召回不是“把历史贴回来”，而是把状态拼出来

**副标题建议：**

判断搜不搜、搜哪层、怎么重排，比把内容召回来更重要

**这一张承载的信息：**

- 召回链路比想象中更容易做坏
- 每轮都全量召回会直接把成本和噪音拉爆
- 召回的终点不是原文，而是可行动状态

**适合直接上图的一句话：**

一个好的 Recall Path，不会把历史整段塞回 prompt，而是只拿回当前任务真正需要的那一小部分状态。

**主链路文案建议：**

`task judge -> candidate retrieval -> rerank -> context pack`

**画面结构建议：**

- 左侧放当前任务卡：
  - continue deployment issue
  - write in my usual style
  - debug like last time
- 中间第一个判断框：
  - need episodic?
  - need semantic?
  - need procedural?
- 第二段做候选召回区：
  - time + keyword + tags
  - semantic retrieval
  - tool / environment filters
- 第三段做 rerank 区：
  - relevance
  - freshness
  - credibility
  - environment match
- 最右侧做 context pack：
  - 2-3 events
  - stable facts
  - one validated procedure
  - next-step summary

**反例提示建议：**

- 全量 history
- 只按向量相似度 Top-K
- 召回后原文整段贴入

**底部金句：**

召回的终点不是文档，而是让模型立刻能用的状态。

---

### 第 6 张：记忆到底该放哪里，不同存储怎么分工

**标题建议：**

记忆不是单库问题，而是存储分工问题

**副标题建议：**

文件系统、关系库、向量索引、图存储、技能库，各自负责不同对象

**这一张承载的信息：**

- 没有一种存储能优雅承接所有记忆
- 真正成熟的设计，是按对象和查询方式拆分存储职责
- 向量库只是召回层，不是完整记忆层

**适合直接上图的一句话：**

别再问“记忆系统该用什么库”，更该问“哪类记忆该放在什么地方”。

**画面结构建议：**

- 中间放一个总标题：`Storage Split`
- 周围放五块存储卡：
  - filesystem
  - relational DB
  - vector index
  - graph store
  - skills library
- 每块卡片都只写三行：
  - 适合存什么
  - 优势是什么
  - 不适合做什么
- 例如：
  - filesystem：notes / snapshots / readable memory files
  - relational DB：events / metadata / version / confidence
  - vector index：semantic recall / approximate match
  - graph store：relations / evolving facts / constraints
  - skills library：reusable procedures
- 底部加一个红色提醒条：
  - vector DB != full memory system

**底部金句：**

好的记忆架构不是单点最强，而是每种存储只做自己最擅长的事。

---

### 第 7 张：最容易被低估的三个模块

**标题建议：**

真正拉开上限的，往往不是主链路，而是这三个模块

**副标题建议：**

冲突处理、压缩、遗忘，决定你的系统能不能长期活下去

**这一张承载的信息：**

- 主链路搭出来不难，难的是长期运行后的秩序
- 冲突、压缩、遗忘做不好，系统很快就会脏、慢、错
- 这三层更像治理能力，而不是存储能力

**适合直接上图的一句话：**

真正会把记忆系统拖垮的，往往不是“没存到”，而是“旧的没处理、长的没压缩、脏的没删掉”。

**画面结构建议：**

- 做成三块并列的治理模块
- 模块 1：Conflict Resolution
  - new fact vs old fact
  - source
  - version
  - confidence
  - current state decision
- 模块 2：Compaction
  - what is done
  - what failed
  - current risk
  - next best action
- 模块 3：Forgetting
  - time decay
  - hit count
  - reuse count
  - replaced by newer memory
- 每块模块底部都放一个“如果没有这层会怎样”的橙色小条
  - 冲突不处理：事实越积越乱
  - 不压缩：上下文越跑越肥
  - 不遗忘：垃圾和有效记忆一起竞争

**底部金句：**

记忆系统能不能长时间可用，取决于它会不会治理自己的过去。

---

### 第 8 张：如果现在就开工，最稳的落地顺序是什么

**标题建议：**

如果今天就开工，最稳的实现顺序是这样

**副标题建议：**

别一上来追求长期记忆大满贯，先把最值钱的五步做出来

**这一张承载的信息：**

- 最小可用路线比“大而全蓝图”更有实操价值
- 先做可回放，再做高价值事实，再做按需召回
- 技能沉淀应该放在最后，而不是第一天就做

**适合直接上图的一句话：**

记忆系统最稳的做法，不是一步到位，而是按价值顺序逐层长出来。

**画面结构建议：**

- 做成一条 5-step roadmap
- Step 1：结构化事件流
  - everything replayable
- Step 2：小而干净的事实层
  - stable only
- Step 3：按需召回
  - retrieve only when needed
- Step 4：压缩、冲突、遗忘
  - governance before scale
- Step 5：技能沉淀
  - turn success into procedure
- 每一步右侧补一个“解决了什么”
  - 可回放
  - 跨会话连续性
  - 成本可控
  - 长任务稳定
  - 经验复用

**右下角总结判断建议：**

- 先把系统做稳
- 再把记忆做深
- 最后才把经验做厚

**底部金句：**

先有干净事件流，才有可信记忆；先有可信记忆，才有可复用能力。

---

## 六、这组图最该让读者记住的三句话

- Agent 记忆系统不是一个库，而是一条工程链路。
- 写入、召回、压缩、冲突处理、遗忘，比“存了多少历史”更重要。
- 真正有用的记忆，不是让 Agent 背更多东西，而是让它下一次更会做事。

---

## 七、封面文生图提示词方向

如果后面要继续往单张文生图脚本细化，封面最适合的方向不是抽象大脑，而是：

**白底技术杂志风，一条横向的 Agent memory runtime blueprint，左侧多源输入，中部写入分流到四层记忆，右侧按需召回并压缩进入当前上下文窗口，底部外挂冲突处理、压缩、遗忘三个治理模块。整体强调系统链路、信息流动和结构秩序，而不是神经网络意象。**

关键词可以保留：

- technical editorial infographic
- system blueprint
- memory write path
- memory recall path
- compaction
- forgetting
- white background
- high information density
- clean structure
