# 追影 — 项目长期记忆

## A. 环境与通道
- Bash coreutils 全缺 → 一律 PowerShell；PowerShell 工具**不回传 stdout**，输出写文件再 Read；中文乱码设 `[Console]::OutputEncoding=UTF8` + `Out-File -Encoding UTF8`。
- 技能更新：`git ls-remote` 判存活（**禁 WebFetch 抓 GitHub 网页**，会误判 404）；npx 直调不通 → node 直调 npx-cli.js；落点是 `.agents/skills` 非 `.workbuddy/skills`，须 robocopy `/E` 同步（不先删，残留用 `[IO.File]::Delete` 清）。
- 版本基线（2026-09-21 更新后，guyin 系升级到 1.0 世代）：write 1.0.0 / setup 0.9.0 / story 1.0.0 / short-write 1.0.0；未变：review 0.9.0 / deslop 0.6.0 / pitch 0.2.0 / analyze 0.5.0 / short-analyze 0.4.0。skills-update 1.0.0 与 tracking-reset 0.1.0 为本机专属技能，不在上游仓库，不随本次更新。

## A2. 2026-09-21 技能包更新重大变化（写章前必读）
- **guyin-write 0.14→1.0 是架构级升级**：从「编排层派 subagent 逐 beat 写」改为「单模型自主执笔」（当前会话自己读前文/定走向/写整章/回看/提事实/跑只读检查）。不再分发 writer/checker 执行层 agent，不再有 full/lean/solo 菜单。
- **关键风险：新版 guyin-write 移除了整个 `scripts/` 目录**（27 个 guyin-check-*.js + guyin-tracking-commit.py + guyin-normalize-punctuation.js + guyin-impact-map.js + lib/），但 SKILL.md 仍引用 `scripts/guyin-author-session.py`、`tracking-commit.py`、`guyin-check-flesh`、`guyin-impact-map`、`guyin-check-reader-signal` 等脚本名 → **脚本引用悬空，上游包自身不一致**。
- 项目 `.claude/hooks/guyin-hook.js` 是自包含部署件（不实调技能库脚本，只在报错文案里提到脚本名），**不受影响**；但写章流程里实际要跑的 `guyin-tracking-commit.py`（publish/check/recover）与检查脚本，新版技能库里已没有实体。
- 旧脚本完整保存在 `C:\Users\PC\.workbuddy\skills\_backup\pre-update-20260921-114650\`，必要时可从备份恢复。
- 结论：**先不要用 1.0 版写新章**，等确认上游脚本去哪了（或从备份把 scripts/ 拷回 guyin-write）再动笔。旧版写章流程（tracking-commit + 章检链）依赖的脚本实体已不在技能库。

## B. 框架状态结论（最高权威，第三版）
- 根因：三模型分离从未真正跑（执行层 model 未配置）→ 实际 solo 直写。**结论：三模型分离 → 单模型三角色分离**（编排保结构/作者保涌现/检查保正确，靠提示词切换），趣味性交给真实读者信号。
- 已作废勿复用：补三道脚本、负相关、框架缺爽文方法论。
- 仍成立：判框架状态必须先读全量文件；纸面修复≠真修复。读者信号机制已存在，缺的是真实正文验证。

## C. 项目硬约定（改了即破契约）
- 复沓锚句：「他把杯把手转了一下，朝外」每章一次；「手放在膝盖上」每章上限一次（老爸肝病指征 ch194 回收，望诊用变体「搁在膝盖上的那只手」）；「看手」四连归 ch001 只引用不重述。
- 叙述层称谓：一律关系称谓，禁全名做主语复读（九岁限知 POV）。
- 世次基准：「他四十七岁那年」=第二世，开篇刚死一次刚回穿；**「往前倒三十八年」是钉死回穿的时间锚（2026-09-18 发现重做 ch001 时误删，须补回）**。卷五 2022-2030，ch194 老爸走 2029，不许推 2038。
- 「吃饭了没」：正方向归小满妈（三次配额）；反方向（老妈对舅舅）ch001 一次性不计配额；老妈签名 tic「吃不吃西瓜」。
- 四类自查：应答动作重复 / 时序倒错 / 主语指代偷换 / 句首缺字。

## D. tracking-commit 关键坑
- commit context 只收 `position/long_term_constraints/active_character_names/continuity_risks`；`recent_chapters`/`next_chapter_commitments` 由工具派生，传了报 unknown。
- 字节上限：delta 硬上限 3072（首章必超，削减顺序地理/场景→次要物证→压缩角色 change）；`delta.result`≤360→`chapter_summaries`≤480；`clean_string_list` 单项≤384；`clean_text` 把 `|` 换 `｜`。
- `character_snapshots` ⊆ `character_changes`（硬校验）；`active_character_names` ⊆ characters 且有快照。
- revision 不能退役/替换 context 项（retire 只能 append），改措辞=追加新条。
- 派生视图必须与 state summary 逐字一致，改完重跑 check。`last_chapter=0` 禁登记伏笔/时间线等；`init` 是清盘唯一正道（输入要求 state 不存在）。
- 补登记用 `backfill`（不增逐章记录），**先读逐章记录确认 ID 水位**（曾误用 G002 覆盖城南早点铺）。

## E. 检查脚本口径
- 不收 `--project`（传了会假绿 exit0）：wordcount/ai-patterns/outline-deliver/repetition/strip/integrity/consistency/degeneration/narrative-asset/outline-copy/slots/verdict/opening-retention。收 `--project`：hook-rotation/pending/rule-conflict/reader-signal/foreshadow-id。
- 判绿看 blocking 数==0，不看 exit code。`outline-copy` 读复沓锚句整块、`outline-deliver` 只读首行 → 功能性原话放续行。
- `foreshadow-id` 用 `/\bF0*(\d{1,4})\b/g` 扫细纲，历史引用 F7→F007 误判，措辞别写 `F\d`。

## F. 内容层重置（用户亲手做，勿逆）
- 删除：正文第001~003章/细纲001/逐章记录001/复沓锚句。规矩：缺失≠缺口，勿从 git/归档恢复。
- `逐章记录/第N章.md` 是 delta 源，删了而 last≥N 则 check 报 chapter delta missing。
- 状态层已重置 ch000（init 通道），备份 `.guyin/state-reset-backup/2026-09-17/`；不变式在 constraints 6 + risks 5 + next_commitments 5 条。
- ch001 已 publish（prose hash12 `0d23bcd2ff90`，state revision 3）。

## G. publish 实操（2026-09-17 首通）
- 清单键：`schema_version=1, run_id, target{chapter,title,mode}, candidate(须在 .guyin/work/{run_id}/ 内), destination(正文/ 下 第0*N章*.md), transaction, baseline[], expected_state_revision, review{mode,conclusion≤900,evidence[]}, check_evidence[]`。
- **证据绑定用小写 hash12**（`sha256[:12]` 小写，逐字含在证据文件字节里；只写大写判未绑定）。baseline 目录条目 hash12 也小写；首发正文基线是 README.md。
- 链：prepared→_write_prose→_commit_tracking→_commit_fingerprint（持锁 node `--commit --under-lock`，**唯一关 fingerprint-arrears 出口**）→_finalize；崩用 recover。
- 落地前必 dry-run（importlib 加载脚本，normalize→merge→render 不写盘）。
- **同一文件多处 Edit 必须串行**（并发丢更新，transaction.json 曾丢 4 处都报成功）；改完 hash12 与 `_publication.json` 对比。
- trial-gate：`--chapter N` 判要写第 N 章；`--chapters` 只给 `--hash` 用且该段正文须全在。

## H. ch001 诊断结论（2026-09-18）
- 见 `大纲/框架诊断_第001章_20260918.md`（v2 聚焦框架机制）。核心三点：①**框架有 `guyin-normalize-punctuation.js`，能识别"——"（正则 `——|—|--+`），但 em-dash severity=advisory（低），`---`=blocking**；门挂 SKILL.md L44（写章循环第 4 步拼接，编排层必跑），**不在 publish prepared 全检**（全检只跑 pending+repetition）——所以"——"漏网=定级低+不在全检+执行层第 4 步漏跑三层叠加。②误删"往前倒三十八年"无人报=框架无"一次性关键锚句/时间锚"登记位，检查门只做后验正确性不做完整性留存。③开头没变=细纲"授权照抄区"无边界+无"保护/重写"开关，保护定稿默认开吞掉"推翻重做"授权。
- **操作纪律（每次写章）**：第 4 步拼接后**必跑 `node guyin-normalize-punctuation.js 候选文件`**（默认写入模式自动清"——"），并**补登记一次性时间锚/世次锚**（框架无此台账，靠自查）。
- 改已发布章的开头**须走 revision 或清盘，不能直接改文件**。
