---
name: game-monitor
description: 监控指定游戏的舆论舆情、运营活动、营销事件与创新玩法。输入游戏名即可从官网、官方社区、TapTap、NGA、机核、游民星空等多渠道采集信息并生成舆情报告。预制了米哈游系（原神、星穹铁道、绝区零）、王者荣耀、明日方舟、和平精英、英雄联盟、鸣潮等热门游戏渠道。当用户提到游戏舆情、游戏口碑、游戏评价、游戏活动、玩家反馈、game sentiment、game reputation 时使用。
version: 1.0.0
author: user
tags: gaming, sentiment, monitor, reputation, events, community, opinion, taptap, nga, gcores
---

# Game Monitor — 游戏舆情监控

输入一个游戏名称，从官网、官方社区、游戏论坛、资讯媒体多渠道采集该游戏的最新动态，分析舆论走向（正面与负面）、运营/营销事件、创新玩法与口碑亮点，输出结构化舆情报告。

## When to use

**Slash command trigger:**
- `/game-monitor <游戏名>` — 例如 `/game-monitor 原神`

**Keyword auto-trigger（任意语言）:**
- "查一下 XX 的舆情"、"XX 最近口碑怎么样"、"XX 有什么活动"、"XX 玩家反馈如何"
- "XX 游戏舆论"、"XX 运营活动"、"XX 最近有什么事件"
- "check XX sentiment"、"what do players think about XX"、"XX reputation"
- "XX 게임 여론"、"XX 평가"

**Also trigger when:**
- User asks about a specific game's current state, player reception, or ongoing events
- User wants a comparison of sentiment for multiple games (run for each game sequentially)

## Preconfigured channels

### Dimension A — Community channels（社区维度）

These are general gaming community / media channels used to gather sentiment and news about ANY game. Reference from `/game-daily` skill.

#### Tier 1 — Game forums & communities（核心社区）

| Channel | Type | Fetch method | Focus |
|---------|------|-------------|-------|
| TapTap | 手游社区 | `WebSearch` for `[游戏名] taptap 评价` + RSSHub `https://rsshub.app/taptap/topic/:id/official` | 玩家评分、评论、官方帖 |
| NGA 玩家社区 | 综合论坛 | `WebSearch` for `[游戏名] site:bbs.nga.cn` + `WebFetch` scrape | 深度讨论、爆料、玩家争论 |
| 百度贴吧 | 社区 | `WebSearch` for `[游戏名] 贴吧 最新` | 大众玩家讨论、热点事件 |
| 米游社 (HoYoLAB) | 米哈游官方社区 | `WebSearch` for `[游戏名] 米游社` + `WebFetch` `https://www.miyoushe.com/` | 米哈游系游戏官方社区 |

#### Tier 2 — Gaming media（游戏媒体）

| Channel | Type | Fetch method | Focus |
|---------|------|-------------|-------|
| Gcores 机核 | RSS `https://www.gcores.com/rss` | `WebSearch` for `[游戏名] site:gcores.com` | 深度评测、文化分析 |
| 游民星空 | RSSHub `https://rsshub.app/gamersky/news` | `WebSearch` for `[游戏名] 游民星空` | 资讯、评测、玩家评论 |
| 3DMGame | RSSHub `https://rsshub.app/3dm/news` | `WebSearch` for `[游戏名] 3dm` | PC 游戏资讯 |
| 触乐 Chuapp | RSS `https://www.chuapp.com/feed` | `WebSearch` for `[游戏名] site:chuapp.com` | 行业深度报道 |
| GameLook | Web scrape | `WebSearch` for `[游戏名] gamelook` | 行业分析、商业报道 |
| 游戏葡萄 | Web scrape | `WebSearch` for `[游戏名] 游戏葡萄` | 产品分析、公司报道 |

#### Tier 3 — International media（海外媒体）

| Channel | Type | Fetch method | Focus |
|---------|------|-------------|-------|
| IGN | RSS `https://feeds.ign.com/ign/all` | `WebSearch` for `[game name] IGN` | Reviews, news |
| Reddit | Forum | `WebSearch` for `[game name] reddit` | Global player discussions |
| GameSpot | RSS | `WebSearch` for `[game name] gamespot` | Reviews, news |
| Polygon | RSS | `WebSearch` for `[game name] polygon` | Culture, features |
| Gematsu | RSS `https://gematsu.com/feed` | `WebSearch` for `[game name] gematsu` | Japan/Asian games |

### Dimension B — Game channels（游戏维度）

Pre-configured source mapping for popular games. When the user queries one of these games, use ALL listed sources in parallel.

#### 米哈游系 (miHoYo / HoYoverse)

**原神 (Genshin Impact)**

| Source type | URL / Method |
|------------|-------------|
| 官网 | `https://ys.mihoyo.com/` (CN) / `https://genshin.hoyoverse.com/` (Global) |
| 米游社 | `WebSearch`: `原神 米游社 最新` |
| TapTap | `WebSearch`: `原神 taptap 评价`; RSSHub: `https://rsshub.app/taptap/topic/168332/official` |
| NGA | `WebSearch`: `原神 site:bbs.nga.cn` (原神版块 fid=650601) |
| 百度贴吧 | `WebSearch`: `原神 原神吧 最新` |
| Reddit | `WebSearch`: `genshin impact reddit` (r/Genshin_Impact) |
| B站 | `WebSearch`: `原神 bilibili 最新动态` |

**崩坏：星穹铁道 (Honkai: Star Rail)**

| Source type | URL / Method |
|------------|-------------|
| 官网 | `https://sr.mihoyo.com/` (CN) / `https://hsr.hoyoverse.com/` (Global) |
| 米游社 | `WebSearch`: `星穹铁道 米游社` |
| TapTap | `WebSearch`: `崩坏星穹铁道 taptap`; RSSHub: `https://rsshub.app/taptap/topic/328943/official` |
| NGA | `WebSearch`: `星穹铁道 site:bbs.nga.cn` (星铁版块) |
| 百度贴吧 | `WebSearch`: `崩坏星穹铁道 贴吧` |
| Reddit | `WebSearch`: `honkai star rail reddit` (r/HonkaiStarRail) |
| B站 | `WebSearch`: `崩坏星穹铁道 bilibili` |

**绝区零 (Zenless Zone Zero)**

| Source type | URL / Method |
|------------|-------------|
| 官网 | `https://zzz.mihoyo.com/` (CN) / `https://zenless.hoyoverse.com/` (Global) |
| 米游社 | `WebSearch`: `绝区零 米游社` |
| TapTap | `WebSearch`: `绝区零 taptap`; RSSHub: `https://rsshub.app/taptap/topic/183019/official` |
| NGA | `WebSearch`: `绝区零 site:bbs.nga.cn` |
| 百度贴吧 | `WebSearch`: `绝区零 贴吧` |
| Reddit | `WebSearch`: `zenless zone zero reddit` (r/ZenlessZoneZero) |
| B站 | `WebSearch`: `绝区零 bilibili` |

#### 腾讯系 (Tencent)

**王者荣耀 (Honor of Kings)**

| Source type | URL / Method |
|------------|-------------|
| 官网 | `https://pvp.qq.com/` |
| TapTap | `WebSearch`: `王者荣耀 taptap`; RSSHub: `https://rsshub.app/taptap/topic/200112/official` |
| NGA | `WebSearch`: `王者荣耀 site:bbs.nga.cn` |
| 百度贴吧 | `WebSearch`: `王者荣耀 贴吧 最新` |
| 营地 | `WebSearch`: `王者荣耀 王者营地 最新活动` (官方辅助 App 社区) |
| B站 | `WebSearch`: `王者荣耀 bilibili` |

**和平精英 (Game for Peace / PUBG Mobile CN)**

| Source type | URL / Method |
|------------|-------------|
| 官网 | `https://gp.qq.com/` |
| TapTap | `WebSearch`: `和平精英 taptap` |
| NGA | `WebSearch`: `和平精英 site:bbs.nga.cn` |
| 百度贴吧 | `WebSearch`: `和平精英 贴吧` |
| B站 | `WebSearch`: `和平精英 bilibili` |

**英雄联盟 (League of Legends)**

| Source type | URL / Method |
|------------|-------------|
| 官网 | `https://lol.qq.com/` (CN) / `https://www.leagueoflegends.com/` (Global) |
| TapTap | `WebSearch`: `英雄联盟手游 taptap` |
| NGA | `WebSearch`: `英雄联盟 site:bbs.nga.cn` (LOL 版块) |
| 百度贴吧 | `WebSearch`: `英雄联盟 贴吧` |
| Reddit | `WebSearch`: `league of legends reddit` (r/leagueoflegends) |
| B站 | `WebSearch`: `英雄联盟 bilibili` |

#### 鹰角系 (Hypergryph)

**明日方舟 (Arknights)**

| Source type | URL / Method |
|------------|-------------|
| 官网 | `https://ak.hypergryph.com/` (CN) / `https://www.arknights.global/` (Global) |
| TapTap | `WebSearch`: `明日方舟 taptap`; RSSHub: `https://rsshub.app/taptap/topic/34599/official` |
| NGA | `WebSearch`: `明日方舟 site:bbs.nga.cn` (方舟版块 fid=650302) |
| 百度贴吧 | `WebSearch`: `明日方舟 贴吧` |
| Reddit | `WebSearch`: `arknights reddit` (r/arknights) |
| B站 | `WebSearch`: `明日方舟 bilibili` |
| PRTS Wiki | `WebSearch`: `明日方舟 prts wiki` (社区 Wiki，活动信息丰富) |

#### 库洛系 (Kuro Games)

**鸣潮 (Wuthering Waves)**

| Source type | URL / Method |
|------------|-------------|
| 官网 | `https://mc.kurogames.com/` (CN) / `https://wutheringwaves.kurogames.com/` (Global) |
| TapTap | `WebSearch`: `鸣潮 taptap`; RSSHub: `https://rsshub.app/taptap/topic/218205/official` |
| NGA | `WebSearch`: `鸣潮 site:bbs.nga.cn` |
| 百度贴吧 | `WebSearch`: `鸣潮 贴吧` |
| Reddit | `WebSearch`: `wuthering waves reddit` (r/WutheringWaves) |
| B站 | `WebSearch`: `鸣潮 bilibili` |

#### 其他热门 (Other popular — extend as needed)

If user queries a game not listed above, the agent should:
1. Use `WebSearch` with `[游戏名] 官网` to find the official website
2. Use `WebSearch` with `[游戏名] taptap` to find its TapTap page
3. Fall back to general community channels (Tier 1 + Tier 2 + Tier 3)
4. Use `WebSearch` with `[游戏名] NGA` or `[游戏名] 贴吧` to find community discussions

## Execution workflow

When triggered, execute the following 4 phases **using parallel subagents** for maximum speed.

### Phase 1 — Game discovery（游戏发现，主 agent）

1. Match user input against the preconfigured game list (Dimension B)
2. If matched → use the pre-configured source mapping
3. If not matched → run discovery:
   - `WebSearch`: `[游戏名] 官网` to find official site
   - `WebSearch`: `[游戏名] taptap` to find TapTap page
   - Proceed with general community channels
4. Determine search keywords (Chinese + English variants):
   - CN: `[游戏名]`, e.g. "原神"
   - EN: `[English name]`, e.g. "Genshin Impact"
   - Aliases: common abbreviations or nicknames

### Phase 2 — Parallel data collection（并行数据采集，3-4 subagents）

Launch **3-4 subagents in parallel** (use Task tool), each responsible for one data dimension:

**Subagent A — Official sources（官方渠道）**
- Fetch official website news/events page via `WebFetch`
- Search `[游戏名] 官方公告 最新活动` via `WebSearch`
- Search `[游戏名] 版本更新 新内容` via `WebSearch`
- If miHoYo game: also search `[游戏名] 米游社 官方公告`
- Collect: news titles, event descriptions, dates, URLs

**Subagent B — Community sentiment（社区舆情）**
- Search `[游戏名] taptap 评价 评分` via `WebSearch`
- Search `[游戏名] NGA 讨论` or `[游戏名] site:bbs.nga.cn` via `WebSearch`
- Search `[游戏名] 贴吧 热议` via `WebSearch`
- Search `[游戏名] 玩家评价 口碑` via `WebSearch`
- Search `[游戏名] reddit` or `[English name] reddit` via `WebSearch`
- Collect: discussion topics, player opinions, complaints, praises, ratings

**Subagent C — Media coverage（媒体报道）**
- Search `[游戏名] 评测 报道` via `WebSearch`
- Search `[游戏名] site:gcores.com` via `WebSearch`
- Search `[游戏名] 游民星空` or `[游戏名] 3dm` via `WebSearch`
- Search `[game name] IGN review` or `[game name] gamespot` via `WebSearch`
- Search `[游戏名] gamelook` or `[游戏名] 游戏葡萄` via `WebSearch`
- Collect: article titles, summaries, scores, URLs

**Subagent D — Events & campaigns（活动与营销）** (optional, launch if subagents limit allows)
- Search `[游戏名] 运营活动 2026` via `WebSearch`
- Search `[游戏名] 联动 合作` via `WebSearch`
- Search `[游戏名] 营销活动 推广` via `WebSearch`
- Search `[游戏名] 新版本 新玩法 创新` via `WebSearch`
- Search `[game name] collaboration event 2026` via `WebSearch`
- Collect: event names, descriptions, reception, URLs

### Phase 3 — Analysis & synthesis（分析综合，主 agent）

After all subagents return, synthesize results across **four analysis dimensions**:

#### Dimension 1: Sentiment overview（舆情概览）
- Classify collected opinions into **positive**, **negative**, and **neutral**
- Identify the dominant sentiment trend
- Note any **polarizing topics** that generate both strong praise and criticism
- Quote representative player comments (paraphrase, don't fabricate)

#### Dimension 2: Event activity（事件与活动动态）
- List current and recent **operational events** (in-game events, updates, patches)
- List **marketing campaigns** (collaborations, promotions, ads)
- List **community events** (contests, fan events, controversies)
- Rate event reception as positive / mixed / negative based on collected feedback

#### Dimension 3: Innovation & gameplay（创新与玩法亮点）
- Note any **new gameplay mechanics** introduced recently
- Note any **innovative features** that are being discussed
- Note any **technical achievements** (graphics, performance, etc.)

#### Dimension 4: Reputation highlights（口碑亮点）
- Identify activities or features with **particularly good reception**
- Note any **viral moments** or positive word-of-mouth
- Note any **awards, records, or milestones** mentioned
- Identify what the community considers the game's **current strengths**

### Phase 4 — Report generation（输出报告，主 agent）

Generate the report as a **Markdown file** (.md) using the template below. Do NOT output the full report inline in chat.

**File output workflow:**
1. Use the `Write` tool to save the report to: `{workspace}/outputs/[游戏名]-舆情报告-[YYYY-MM-DD].md`
   - Replace `[游戏名]` with the actual game name (Chinese)
   - Replace `[YYYY-MM-DD]` with the current date
   - `{workspace}` refers to the QoderWork workspace output directory (e.g. `C:\Users\<user>\.qoderwork\workspace\<session>\outputs`)
2. Use `mcp__qw-builtin__present_files` to present the generated .md file to the user as an interactive card
3. In the chat response, provide only a **brief summary** (3-5 sentences) of the key findings, followed by a `file://` link to the report file. Do NOT repeat the full report content in chat.

**For multi-game comparison**, save as: `{workspace}/outputs/[游戏A]-vs-[游戏B]-舆情对比-[YYYY-MM-DD].md`

## Output format

The report is written as a **.md file** via the `Write` tool. The following is the file content template. All content below is the file body — it is NOT output directly in chat.

```markdown
# [游戏名] 舆情监控报告

> 采集时间：[YYYY-MM-DD HH:MM]
> 数据来源：[列出本次成功采集的所有渠道名称]

---

## 一、舆情概览

**整体舆论倾向：** [正面为主 / 负面为主 / 褒贬不一 / 相对平稳]

### 正面声音
[列出 2-5 条主要正面舆论点，每条包含具体内容和来源渠道]
- **[正面观点标题]**：[具体描述，2-3 句]（来源：[渠道名]）

### 负面声音
[列出 2-5 条主要负面舆论点，每条包含具体内容和来源渠道]
- **[负面观点标题]**：[具体描述，2-3 句]（来源：[渠道名]）

### 争议焦点
[如有明显争议话题，列出 1-3 个，说明正反两方观点]

---

## 二、活动与事件动态

### 运营活动
[当前/近期的游戏内运营活动]
- **[活动名称]**：[活动简介] | 玩家反馈：[好/一般/差] | [来源链接]

### 营销事件
[市场推广、联动合作、品牌营销等]
- **[事件名称]**：[事件简介] | 效果评估：[描述] | [来源链接]

### 社区事件
[社区热点事件、争议、玩家自发活动等]

---

## 三、创新与玩法亮点

[近期新增的游戏机制、创新玩法、技术突破等]
- **[亮点名称]**：[描述] — [社区反应]

---

## 四、口碑亮点

[效果特别好、口碑特别佳的活动或内容]
- **[亮点标题]**：[详细描述为什么受到好评] | [来源链接]

---

## 五、数据来源明细

| 渠道 | 状态 | 采集到的信息条数 |
|------|------|----------------|
| [渠道名] | 成功 / 失败 | [N] 条 |

---

*本报告基于公开渠道自动采集，仅供参考。*

## Sources

[列出本次采集引用的所有来源链接，格式为 Markdown 超链接]
- [来源名称](URL)
- ...
```

## Search keyword strategy

For each game, generate search queries in **both Chinese and English**:

### Chinese queries (always use)
- `[游戏名] 最新` — general latest news
- `[游戏名] 玩家评价 口碑` — player reviews
- `[游戏名] 差评 吐槽 问题` — negative feedback
- `[游戏名] 好评 推荐` — positive feedback
- `[游戏名] 活动 更新 版本` — events and updates
- `[游戏名] 联动 合作 营销` — collaborations and marketing
- `[游戏名] 新玩法 新模式 创新` — gameplay innovations

### English queries (use for globally-known games)
- `[English name] review` — reviews
- `[English name] news update` — latest news
- `[English name] community reaction` — community sentiment
- `[English name] event collaboration` — events

### Time-scoping
- Append `2026` or `最新` to queries to ensure fresh results
- In `WebSearch`, prefer results from the last 30 days
- For RSS feeds, filter articles from the last 7 days

## Rules

- **Language**: Match the user's language. Chinese input → Chinese report. English input → English report. Translate source content as needed.
- **Factual**: Only report information found in sources. Do NOT fabricate events, ratings, or player quotes. If unsure, say "有玩家提到…" or "据部分报道…"
- **Balance**: Always present both positive and negative sentiment, even if one side dominates. Do not censor negative opinions.
- **Source attribution**: Every claim must reference its source channel. Use `[来源: 渠道名]` inline.
- **Freshness**: Prioritize information from the last 2 weeks. Mark older information with "（较早）" if included.
- **Dedup**: If the same event is reported by multiple sources, merge into one entry and list all source names.
- **Parallelism**: ALWAYS use subagents (Task tool) for data collection to maximize speed. Launch at least 3 subagents for Phase 2.
- **No opinion injection**: The report summarizes what the community and media say. Do NOT add the agent's own opinions or recommendations.
- **TapTap ID discovery**: If a game's TapTap ID is unknown, search TapTap first: `WebSearch` `[游戏名] site:taptap.cn` or `WebFetch` `https://www.taptap.cn/search/[游戏名]` to find the numeric ID.
- **Graceful degradation**: If a source fails, skip it silently and note "失败" in the data source table. Never block the report because one source is unavailable.
- **File output (MANDATORY)**: The full report MUST be saved as a `.md` file using the `Write` tool and presented via `mcp__qw-builtin__present_files`. NEVER output the full report as plain text in the chat. The chat should only contain a brief 3-5 sentence summary and a `file://` link to the report.

## Error handling

| Situation | Response |
|-----------|----------|
| Game not found in preconfigured list | Run discovery (Phase 1 fallback), proceed with general channels |
| Official website unreachable | Skip, rely on community and media sources |
| TapTap RSS unavailable | Use `WebSearch` for `[游戏名] taptap` as fallback |
| NGA requires login | Use `WebSearch` for `[游戏名] site:bbs.nga.cn` instead of direct `WebFetch` |
| All Tier 1 community channels fail | Use media channels + WebSearch as fallback |
| Subagent timeout | Collect results from completed subagents, note missing dimensions |
| No results found at all | "未能找到该游戏的近期舆情信息，请确认游戏名称是否正确，或稍后再试。" |
| Non-existent game | "未找到名为「XX」的游戏，请检查名称或提供该游戏的英文名称。" |

## Advanced: comparing multiple games

If the user asks to compare sentiment across multiple games (e.g., "对比原神和鸣潮的舆情"):

1. Run Phase 1-3 for each game (can parallelize across games too)
2. In Phase 4, generate individual reports PLUS a comparison section:
   ```
   ## 对比总结
   | 维度 | [游戏A] | [游戏B] |
   |------|---------|---------|
   | 整体舆情 | ... | ... |
   | 活动力度 | ... | ... |
   | 口碑亮点 | ... | ... |
   | 主要争议 | ... | ... |
   ```

## Advanced: periodic monitoring

If the user wants regular monitoring of a game, suggest using QoderWork's scheduled task (cron) feature:
- Use `mcp__qw-builtin__qoder_cron` tool to set up a recurring task
- Example: run every Monday morning at 9am to generate a weekly sentiment report
- The cron job's `payload.message` should describe the task: "查询 XX 游戏的舆情并生成报告"

## Integration with /game-daily

This skill complements `/game-daily`:
- `/game-daily` → broad industry news across all games
- `/game-monitor <游戏名>` → deep dive into one specific game's sentiment and events

If the user asks for both, run them in parallel and present combined results.
