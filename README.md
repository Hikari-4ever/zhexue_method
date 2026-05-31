# 玄学术数

## 你的命，几千行 Python 算完了。

这不是你在网上看到的那些"输入生日→输出几句废话"的 toy。这是一个**从底层硬编码的玄学引擎**——八字、紫微、梅花、奇门、六壬、称骨，全部是算法，全部可复现，全部开源。

想算八字？跑一行。
想看紫微命盘？跑一行。
想知道今天出门会不会踩狗屎？跑一行。

**对，就是这么回事。**

---

## 它能算什么

| 你想干嘛 | 跑什么 |
|----------|--------|
| 完整八字+59种神煞+大运流年流月流日流时 | `python3 bazi.py ...` |
| 紫微斗数14主星+辅星+39小星+自化 | `python3 ziwei.py ...` |
| 梅花易数起卦 | `python3 meihua.py ...` |
| 奇门遁甲时家转盘 | `python3 qimen.py ...` |
| 大六壬三传天将 | `python3 liuren.py ...` |
| 称骨算命 | `python3 chenggu.py ...` |
| 一站式入口 | `python3 run.py ...` |

---

## 八字能有多硬核

- **59种神煞**，78条规则引擎，年干/日干双查、月支起查、旬空、纳音、特定日柱匹配——比市面上90%的App还全
- **节气精确月柱**：立春不是2月4号就完事了，是精确到分钟的节气切换
- **干支流通**：天干生克五合、地支六合三合六冲三刑六害——写死了还不如算出来
- **宫位六亲**：你的爸在哪柱、你妈在哪柱、你未来对象在哪柱——不是猜的
- **大运+流年+流月+流日+流时**：从你出生到死，120年大运你都能查
- **用神旺衰**：身强还是身弱，用神是木还是火——定量计算，不靠感觉

---

## 装到你的 Agent 里

这些脚本本身只是 Python 文件，但要让 AI agent 知道怎么用它，需要一个 **skill 定义文件**（SKILL.md）。下面是各平台的装法：

### Hermes Agent

```bash
# 把技能装到你的 hermes profile 里
git clone https://github.com/Hikari-4ever/zhexue_method.git ~/.hermes/skills/zhexue-methods

# 确保脚本可执行
chmod +x ~/.hermes/skills/zhexue-methods/scripts/*.py
```

然后在对话里说一句"加载玄学术数 skill"，Hermes 就会自动读取 SKILL.md，知道有哪些脚本、怎么用。

### Claude Code

```bash
# 克隆到项目里，或者加到你的 claude.md 里
git clone https://github.com/Hikari-4ever/zhexue_method.git ~/.claude/skills/zhexue-methods/

# 在 CLAUDE.md 里加一行：
# 我有玄学术数工具在 ~/.claude/skills/zhexue-methods/scripts/，八字/紫微/梅花/奇门/六壬/称骨都能算。问我就用。
```

### OpenCode

```bash
# 加到 skills 目录
git clone https://github.com/Hikari-4ever/zhexue_method.git ~/.opencode/skills/zhexue-methods/
```

### Codex CLI

```bash
# 代码放哪里都可以，在提示词里告诉 Codex 路径就行
git clone https://github.com/Hikari-4ever/zhexue_method.git ~/zhexue-methods/

# 然后跟 Codex 说："用 ~/zhexue-methods/scripts/ 里的工具给我算一下八字"
```

### 通用（哪个 agent 都不用）

```bash
cd scripts/
python3 run.py bazi 2000 1 1 12 0 male
# 你的八字就出来了，不需要任何 agent
```

---

## 这个项目本来不是给你用的

这套代码最开始是写给我自己用的——我是 Hikari-4ever，一个没事喜欢拿 Python 算命的玄学程序员。

我受够了那些：
- 看一句话还要你充会员的App
- 算出来全是"贵人相助""事业有成"的废话
- 没有任何一个告诉我 **这个结论是怎么来的**

所以我把文墨天机、子平八字、梅花易数这些东西全部拆了，用代码实现了。

**我不保证你的人生会变好。但我保证你算出来的每一行都有依据。**

---

## 一行都不想写？行

```bash
python3 run.py bazi 2000 1 1 12 0 male
```

就会出来你完整的人生说明书。别问为什么是这个日子。自己去查那天出生的人后来怎么样了。

---

## 友情提示

1. **称骨必须用农历**。公历往里塞，出来的结果你自己负责。
2. **紫微有两种流派**。顺月逆时 vs 逆月顺时，差很多。我们默认走文墨天机的标准。
3. **算出来的结果别太信**。命理这东西，信则有不信则无。但如果你算出来是大富大贵的命，记得请我喝奶茶。

---

## 技术栈

- Python 3
- 节气数据：1800-2100年共302年，手动校对
- 神煞规则：59种，78条匹配规则
- 称骨权重：逐元素对比过 Java 源码，没有抄错

**代码哲学：** 能用算法解决的，绝不写 if-else。写了的 if-else，一定有注释说明为什么。

---

## 关于作者

Hikari-4ever，一个写代码和算命五五开的普通人。白天写 bug，晚上写八字。

如果你觉得有用——star 就好，不用请我吃饭。

如果你觉得没用——那一定是你的生辰八字还没算对。
