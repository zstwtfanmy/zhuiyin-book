# 章检证据（ch001 候选稿 · 发布前）

- 候选 sha256 全量：0D23BCD2FF900E05F89E2FFFF12402140F0758374AC92E26184D612175C47416
- **候选 hash12：0D23BCD2FF90**（小写：0d23bcd2ff90）
- 候选（唯一产物）：`.guyin/work/ch001-20260917/candidate.md`
- 受检副本：`.guyin/_check/第001章_他不是要睡觉.md`（与候选逐字节相同；章检脚本按「第N章」文件名＋向上 3 层找 `大纲/` 定位细纲，隔离工作区 `.guyin/work/{run_id}/` 太深会静默跳过，故经暂存副本受检）
- 细纲：`大纲/细纲_第001章.md`（字数目标 3400，区间 3200-3500，章检下限 3200）

## 前置门

- tracking-commit check：{"last_committed_chapter": 0, "state_revision": 0}（EXIT=0，无时滞）

## 章检链（发布前·对工作区候选）

### strip 成稿剥离门 K3

strip: 1 file(s) clean
- EXIT=0

### degeneration

（无输出＝干净）
- EXIT=0

### integrity

（无输出＝干净）
- EXIT=0

### ai-patterns

D:\readbook-workspace\追影\.guyin\_check\第001章_他不是要睡觉.md:3:1: [editorial/advisory] prose-fragment-ratio: 碎化率显著（观测值，需结合上下文判断）：叙述段 124 个，61 个≤15字（49%，参考阈值 25/40%）——短段成串是文体启发式信号不是必然错误；刻意的短镜头、低压过场可成立。若确属把「带过」写成了「切碎」，修法是恢复必要连接与句群，不是机械并段注水（Fw-02/v3-A1） (面很烫。 | 她说。 | 那是他这辈子最后一次开口。 | 他后悔了很久。 | 不是后悔那半句话。 | 他这辈子都想不起来，那句话是什么。)
D:\readbook-workspace\追影\.guyin\_check\第001章_他不是要睡觉.md:13:1: [editorial/advisory] em-dash: 破折号按功能复核（editorial，不阻断）：打断→动作 beat/短句，拖长音→省略或动作，插入说明→逗号/冒号；勿一律改句号。 (——)
D:\readbook-workspace\追影\.guyin\_check\第001章_他不是要睡觉.md:17:1: [editorial/blocking] not-is-comparison: 高频 AI 对比句式；删掉否定铺垫，直接写后项，或改成动作/细节呈现。 (不是后悔那半句话。 是更早的那天)
D:\readbook-workspace\追影\.guyin\_check\第001章_他不是要睡觉.md:23:1: [editorial/advisory] em-dash: 破折号按功能复核（editorial，不阻断）：打断→动作 beat/短句，拖长音→省略或动作，插入说明→逗号/冒号；勿一律改句号。 (——)
D:\readbook-workspace\追影\.guyin\_check\第001章_他不是要睡觉.md:87:1: [editorial/advisory] micro-action-tic: 微动作复读：「了下/了一下」式轻量补语 18 处（8.2/千字）；同一反应模板高密度复现是机械指纹，合并动作 beat、换具体细节，别每个动作都补一个轻反应尾巴。 (了一下 了两下 了一阵 了一声 了一道 了一会)
D:\readbook-workspace\追影\.guyin\_check\第001章_他不是要睡觉.md:1:1: [editorial/advisory] dialogue-zero-information: 对话零信息嫌疑（ch1-3 启发式）：主角「沈亦舟」邻近的发问对白 0 句、全体对白长度中位仅 5 字——主角只被问/只短答，没有主动索取信息或抛出筹码；开篇需要主角主动发起的对话。启发式非精确，刻意沉默主角可走豁免（Fw-05）。 ()
- EXIT=0

### narrative-asset

（无输出＝干净）
- EXIT=0

### consistency

（无输出＝干净）
- EXIT=0

### outline-copy

（无输出＝干净）
- EXIT=0

### outline-deliver 承诺交付 S3/S4/R1

outline-deliver: 1 chapter(s) contracts honored
- EXIT=0

### authority-leak 作者性字面 H2

authority-leak: no literal leakage found (1 file(s) scanned)
- EXIT=0

### wordcount J1 双口径下限

wordcount: 1 file(s) within limits [3200, 6000]
- EXIT=0

### repetition 复读雷达+指纹库

# 指纹库为空（首章或未 --commit 过）：11 段叙述段暂无历史可比
.guyin\_check\第001章_他不是要睡觉.md:1:1: [hard/blocking] fingerprint-arrears: 指纹库欠账：库登记至第 0 章，受检正文至第 1 章——第 1 章起未固化，先跑 --commit 补齐再过章检（写章循环第 6 步：追踪提交+指纹固化为原子双命令）
- EXIT=1

### beat 确定性预检

D:\readbook-workspace\追影\.guyin\_check\第001章_他不是要睡觉.md:129:1: [editorial/advisory] dialogue-run: 连续 4 行纯对白（剥引号后叙述余量 ≤4 字）——观测值，需结合上下文判断：纯对话场景可成立；若读感单调，可在行间插入动作/环境（半自动检测）
D:\readbook-workspace\追影\.guyin\_check\第001章_他不是要睡觉.md:175:1: [editorial/advisory] dialogue-run: 连续 4 行纯对白（剥引号后叙述余量 ≤4 字）——观测值，需结合上下文判断：纯对话场景可成立；若读感单调，可在行间插入动作/环境（半自动检测）
D:\readbook-workspace\追影\.guyin\_check\第001章_他不是要睡觉.md:219:1: [editorial/advisory] dialogue-run: 连续 6 行纯对白（剥引号后叙述余量 ≤4 字）——观测值，需结合上下文判断：纯对话场景可成立；若读感单调，可在行间插入动作/环境（半自动检测）

[summary] 脚本已查：Q2
[summary] 语义审读（动机/兑现/承接）归完整章审读（SKILL.md 4a）——反应与后果可隐含可延迟
- EXIT=0

## 项目级门

- pending U1 待审清零：pending: 26 row(s) in scope, all terminal（EXIT=0）
- rule-conflict Fw-04：rule-conflict: ledger present, no unadjudicated conflict rows（EXIT=0）
- foreshadow-id Fw-09 C2：foreshadow-id: no ledger data rows (silent)（EXIT=0，伏笔台账空表＝首章未登记）
- trial-gate 验收检查点门 ch1：（无输出＝通过）（EXIT=0）
