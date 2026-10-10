# 项目网站每日内容更新契约

## 范围与来源

只写 GitHub 仓库 `Meeeee520/python` 和 `Meeeee520/DataStructure` 的 main。不得修改、清空或重新部署原网站。项目网站私密托管，在线读取两个公开仓库的学习内容，不接收个人作答记录。

先读取两仓库 `LEARNING_PLAN.md`、`DAILY_UPDATE.md`、`PROJECT_PLAN.md`、本文件、`projects/index.json`、最近的 Markdown 笔记与项目详情；用户最新规划优先。时区使用 Asia/Shanghai。当日笔记与原网站的五道题仍按既有契约分别生成，不用项目替代笔记，不要漏掉周日。

## 工作日与周末规则

- 周一至周五，每天生成一个 Python 主项目（45–60 分钟），以及同一场景的 Java 可选加练（约 20 分钟）。Python 使用当日已学主题；Java 按当日数据结构主题，不能强加未来知识。
- 周六生成一个周末综合项目，周日继续同一个项目。项目回用本周周一至周五知识；周日当天新知识可作为第二阶段扩展。两天合计 Python 约 2.5–3 小时、Java 约 35–45 分钟。
- 周末 ID 固定为 `weekend-YYYY-MM-DD`，日期是周六；日常 ID 为 `daily-YYYY-MM-DD`。跨月周末也继续周六 ID，文件放周六所在月份。永远不要换 ID 或任务/测试/回忆条目 ID 来刷新内容，否则会使已有进度看起来消失。
- 已有完整内容只检查链接与准确性；周日不再创建第二个项目，不重复发布 Saturday 项目。部分成功只补缺失。不要因为内容写入失败删历史。
- 既有指数中未来 `ready:false` 是项目预告，不是完整内容。生成完成且两仓库都读回验证后才将该条目设为 `ready:true`。
- 每周共用 12–15 小时。主项目优先，Java 加练可选；原网站五道题用于补弱，不要求再全量叠加。
- 十月后：优先用户的新规划；缺失时沿已知主线合理延伸并明确注明。追加下一周预告与当天项目，保持周末合并规则，不将推导安排冒充原聊天原文。

## 文件与发布顺序

两个仓库都保存：

- `projects/YYYY-MM/<project-id>.json`：各自学习线详情；Python `track:"python"`，DataStructure `track:"java"`。
- `projects/YYYY-MM/<project-id>.md`：美观可读的项目手册，包含目标、先修、每步为什么、本地运行、自测、回忆和折叠参考实现。
- `projects/index.json`：同一份合并目录。网站以 Python 仓库的此文件为主入口。

顺序：先写两仓库项目 JSON 与 Markdown，核对正常和有意义的边界样例，提交后读回；然后更新两仓库目录中的单条 readiness 及 README 项目入口。索引路径只接受 ASCII 字母数字、横线和下划线，例如 `projects/2026-10/weekend-2026-10-10.json`。源文件更新无需重新部署网站。不得上传任何用户代码草稿、自测输出或私人复盘。

## 索引 schemaVersion 1

顶层 `schemaVersion:1`、`updatedAt`（上海当日日期）、`projects` 数组。每个条目必须包含：

`id`、`startDate`、`endDate`、`kind`（daily/weekend）、`title`、`description`、`concepts`（Python 字符串数组）、`javaConcepts`（字符串数组）、`minutes`、`javaMinutes`、`pythonPath`、`javaPath`、`guidePath`、`javaGuidePath`、`ready`（布尔值）。

各 path 以 `projects/YYYY-MM/` 开头；Python/Java path 位于对应仓库，相同项目使用相同 ID。日常起止日期相同；周末起于周六、止于周日，一条记录覆盖两天。按 startDate 排序，每个 ID 唯一。

## 详情 schemaVersion 1

参考已验证的 `weekend-2026-10-10.json` 和 `daily-2026-10-12.json`。顶层包含：

- `schemaVersion:1`、`projectId`、`track`、`title`、`goal`。
- `prerequisites` 字符串数组；`filename` 必须与 Java public class 同名；`runCommand` 是 Mac 终端运行方式。
- `starter` 起始代码、`solution` 完整参考代码、`solutionExplanation` 中文解释数组。
- `steps`：3–5 项，周末可 5–7 项；每项 `{id,day,title,instruction,hint,knowledge}`。day 是实际任务日期，周末包含两天；ID 稳定，knowledge 为字符串数组。
- `tests`：正常与空数据/单元素/非法值等真实边界；每项 `{id,label,input,output,purpose}`。网站只核对粘贴输出，不执行代码。Git 等操作类任务也提供可确定的输出小脚本作为验收；不能把不确定的 commit SHA、用户名等要求成固定输出。
- `recall`：2–3 项 `{id,question,answer}`，引导主动回忆。
- `sources`：实际核对过的官方资料，`{title,url,attribution}`。项目为原创/改编必须明确说明，不能虚构原题出处。

标识字段限 ASCII 字母数字、横线和下划线且不超 80 字符。参考代码按对应 Python/Java 运行，核对每个自测输出；明显错误修复时保留进度字段 ID。JSON 使用真实换行字符串，Markdown 代码围栏闭合。

## 验证与失败处理

GitHub 写入前读取当前文件 SHA，保留用户新增内容与已有目录。写入后读回，不把未来准备或部分成功报告为完成。用已连接 GitHub 工具完成写入；网站自动任务无需访问作者的本地目录。连接失效时报告实际阻塞；一条学习线失败仍完成另一条笔记，项目目录暂不置 ready。

简短报告当天两份笔记链接与项目入口。周日说明“继续周六同一个项目”。不要说用户已经完成项目，不替用户勾选步骤。
