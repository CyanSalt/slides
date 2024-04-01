---
titleTemplate: '%s - CyanSalt'
author: CyanSalt
keywords: Game Theory

transition: slide-left
mdc: true
fonts:
  sans: 'Xiaolai SC'
  mono: 'Xiaolai Mono SC'

hideInToc: true
class: text-center
---

# 谈谈博弈论

如何在重复的博弈中获胜

<HomeButton />

<HomeFooter />

---
hideInToc: true
class: 'flex flex-col items-center'
---

# 谈谈博弈论

如何在重复的博弈中获胜

<Toc maxDepth="1" />

<br>

全文参阅 [《谈谈博弈论：如何在重复的博弈中获胜》](https://bytedance.larkoffice.com/docx/Fs90dE0KOoUf1lx0uFScc0EYnJQ)

---

<script lang="ts" setup>
import { Brain, Computer } from 'lucide'
import { RIcon } from 'roughness'
</script>

<div class="relative h-full flex justify-around items-center">
  <RIcon
    :icon="Brain"
    class="text-[8rem]"
    :style="{ '--r-icon-line-width': 1 }"
  />
  <RIcon
    :icon="Computer"
    class="text-[8rem]"
    :style="{ '--r-icon-line-width': 1 }"
  />
  <div v-click class="absolute inset-auto text-center">
    <img
      class="h-1/2"
      src="/von-neumann.png"
      alt="John von Neumann"
    >
    <p>冯·诺伊曼</p>
  </div>
</div>

---
title: 什么是博弈论？
class: 'flex flex-col items-center'
---

# 谈谈博弈论

如何在重复的博弈中获胜

<Toc maxDepth="1" />

<style>
:deep(.router-link-exact-active) {
  color: var(--slidev-theme-primary);
  font-weight: bold;
}
</style>

---
class: 'flex flex-col items-center'
---

<p v-click.hide>

> 子曰：“饱食终日，无所用心，难矣哉！不有博弈者乎，为之犹贤乎已。”

</p>

<style>
.slidev-vclick-hidden-explicitly {
  opacity: 0.5 !important;
}
</style>

<p v-after>

> 孔子说呀，“每天吃饱了啥也不干，让人难蚌！不是可以掷色子下围棋啥的吗，也比啥也不干强吧。”

</p>

<p v-after>
  <img
    class="h-60"
    src="/confucius.jpg"
    alt="Confucius"
  >
</p>

---
hideInToc: true
layout: statement
---

# 博弈论

一种探究<span v-mark.orange>在竞争关系中争取利益的策略</span>的学科。

---
hideInToc: true
layout: two-cols-header
---

# “交闪不杀”

<style>
.two-cols-header {
  grid-template-rows: 1fr 2fr;
}
</style>

::left::

<div v-click class="text-center">
  <img
    class="h-60 m-auto"
    src="/example-1.jpg"
    alt="Example"
  >
  <p>（一个反例）</p>
</div>

::right::

<div v-click class="text-center">
  <iframe src="https://player.bilibili.com/player.html?aid=493710936&bvid=BV1iN411T7pX&cid=1337693633&p=1&autoplay=0" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"></iframe>
</div>

---
hideInToc: true
layout: statement
---

## 博弈 === 竞争 ？

---
title: 囚徒困境
class: 'flex flex-col items-center'
---

# 谈谈博弈论

如何在重复的博弈中获胜

<Toc maxDepth="1" />

<style>
:deep(.router-link-exact-active) {
  color: var(--slidev-theme-primary);
  font-weight: bold;
}
</style>

---
layout: two-cols
layoutClass: gap-8
---

<div class="h-full flex flex-col justify-center">
  <img class="h-60" src="/robbed-bank.png" alt="Robbed Bank">
</div>

::right::

<div class="h-full flex flex-col justify-center">
  <img class="h-60" src="/prisoners.jpg" alt="Prisoners">
</div>

---

<div class="h-full flex flex-col justify-center items-center">
  <img class="h-60" src="/prisoners-2.png" alt="Prisoners">
</div>

---
layout: center
---

<script lang="ts" setup>
import { Ellipsis, X } from 'lucide'
import { RIcon, RSpace, RTable, RTableColumn, RText } from 'roughness'
</script>

<RTable :rows="[1, 2, 3]" :header="false">
  <RTableColumn v-slot="{ row }" name="A">
    <template v-if="row === 2">
      <RSpace>
        你
        <RIcon type="info" :icon="Ellipsis" />
      </RSpace>
    </template>
    <template v-else-if="row === 3">
      <RSpace v-mark.orange.circle="3">
        你
        <RIcon type="error" :icon="X" />
      </RSpace>
    </template>
  </RTableColumn>
  <RTableColumn v-slot="{ row }" name="B">
    <template v-if="row === 1">
      <RSpace>
        老六
        <RIcon type="info" :icon="Ellipsis" />
      </RSpace>
    </template>
    <template v-else-if="row === 2">
      <RSpace vertical>
        <RText>你 = 251 天</RText>
        <RText>老六 = 251 天</RText>
      </RSpace>
    </template>
    <template v-else-if="row === 3">
      <RSpace vertical>
        <RText v-mark.green>你 = 无罪</RText>
        <RText>老六 = 10 年</RText>
      </RSpace>
    </template>
  </RTableColumn>
  <RTableColumn v-slot="{ row }" name="C">
    <template v-if="row === 1">
      <RSpace v-mark.red.circle="4">
        老六
        <RIcon type="error" :icon="X" />
      </RSpace>
    </template>
    <template v-else-if="row === 2">
      <RSpace vertical>
        <RText>你 = 10 年</RText>
        <RText>老六 = 无罪</RText>
      </RSpace>
    </template>
    <template v-else-if="row === 3">
      <RSpace vertical v-mark.red.circle="5">
        <RText v-mark.green>你 = 5 年</RText>
        <RText>老六 = 5 年</RText>
      </RSpace>
    </template>
  </RTableColumn>
</RTable>

---
level: 2
layout: center
class: text-center
---

# 纳什均衡

<div class="relative">
  <img v-click="[1, 2]" class="h-60 w-full absolute object-contain" src="/nashor.jpeg" alt="Nashor">
  <img v-click="2" class="h-60" src="/nash.jpeg" alt="Nash">
</div>

---
hideInToc: true
layout: statement
---

# 均衡 !== 整体最优

（甚至不是局部最优）

---
level: 2
layout: center
class: text-center
---

# 帕累托最优

<img v-click class="h-60" src="/pareto-optimality.png" alt="Pareto Optimality">

---
level: 2
layout: center
class: 'flex flex-col items-center'
---

# 但是，为什么？

<v-clicks>

- 信息差

- ？

</v-clicks>

---
level: 2
layout: center
class: text-center
transition: slide-right
---

# 公地悲剧

<img v-click class="h-60" src="/tragedy-of-the-commons.jpg" alt="Tragedy of the Commons">

---
level: 2
hideInToc: true
layout: center
class: 'flex flex-col items-center'
---

# 但是，为什么？

- 信息差

<v-clicks>

- 利益关系

</v-clicks>

---
title: 重复博弈
class: 'flex flex-col items-center'
---

# 谈谈博弈论

如何在重复的博弈中获胜

<Toc maxDepth="1" />

<style>
:deep(.router-link-exact-active) {
  color: var(--slidev-theme-primary);
  font-weight: bold;
}
</style>

---
hideInToc: true
layout: center
class: 'relative h-full flex flex-col justify-center items-center'
---

# 如果…

<div class="relative h-full flex flex-col justify-center items-center">
  <template v-for="i in 20" :key="i">
    <img v-click="1" class="absolute h-60" :style="{ transform: `translate(${i}rem, ${i}rem)`, 'transition-delay': `${i * 100}ms` }" src="/prisoners-2.png" alt="Prisoners">
  </template>
  <img class="h-60" src="/prisoners-2.png" alt="Prisoners">
</div>

---
layout: center
---

<script lang="ts" setup>
import { RIcon, RSpace, RTable, RTableColumn, RText } from 'roughness'
</script>

<RTable :rows="[1, 2, 3]" :header="false">
  <RTableColumn v-slot="{ row }" name="A">
    <template v-if="row === 2">
      <RSpace v-click="1">
        你
        <RText type="success">合作</RText>
      </RSpace>
    </template>
    <template v-else-if="row === 3">
      <RSpace v-click="2">
        你
        <RText type="error">背叛</RText>
      </RSpace>
    </template>
  </RTableColumn>
  <RTableColumn v-slot="{ row }" name="B">
    <template v-if="row === 1">
      <RSpace v-click="1">
        对手
        <RText type="success">合作</RText>
      </RSpace>
    </template>
    <template v-else-if="row === 2">
      <RSpace vertical v-click="1">
        <RText>你 +3 分</RText>
        <RText>对手 +3 分</RText>
      </RSpace>
    </template>
    <template v-else-if="row === 3">
      <RSpace vertical v-click="2">
        <RText v-mark.blue="5">你 <RText type="success">+5</RText> 分</RText>
        <RText>对手 <RText type="error">-1</RText> 分</RText>
      </RSpace>
    </template>
  </RTableColumn>
  <RTableColumn v-slot="{ row }" name="C">
    <template v-if="row === 1">
      <RSpace v-click="3">
        对手
        <RText type="error">背叛</RText>
      </RSpace>
    </template>
    <template v-else-if="row === 2">
      <RSpace vertical v-click="3">
        <RText>你 <RText type="error">-1</RText> 分</RText>
        <RText>对手 <RText type="success">+5</RText> 分</RText>
      </RSpace>
    </template>
    <template v-else-if="row === 3">
      <RSpace vertical v-click="4">
        <RText v-mark.blue="5">你 <RText type="warning">+1</RText> 分</RText>
        <RText>对手 <RText type="warning">+1</RText> 分</RText>
      </RSpace>
    </template>
  </RTableColumn>
</RTable>

<br>

<p class="text-right" v-click="6">但是…</p>

---
level: 2
hideInToc: true
layout: center
class: 'flex flex-col items-center'
---

# 但是…

<v-clicks>

- 多重纳什均衡

- 两位以上的玩家

- <span class="text-2xl">不知道比赛的总场次</span>

</v-clicks>

<br>

<script lang="ts" setup>
import { ArrowRight } from 'lucide';
import { RIcon, RSpace } from 'roughness'
</script>

<p v-click>
  <RSpace align="center">
    <Link to="pirate-game">海盗分金币</Link>
    <RIcon :icon="ArrowRight" />
  </RSpace>
</p>

---
level: 2
---

# 可行的策略

<v-clicks>

- 罗伯特·阿克塞尔罗德

- 数学家、经济学家、政治学家、心理学家… * 14

</v-clicks>

<div v-click class="flex flex-col justify-center items-center">
  <img class="h-60" src="/experts.png" alt="Experts">
</div>

---

<div class="grid grid-cols-2 grid-rows-2 gap-4">

<div v-click>

## Sample

默认合作，如果对手连续两次背叛，则下一次也会背叛。

<p v-click="2">“宽容”</p>

</div>

<div v-click="3">

## DOWNING

测试对手是否总是倾向于合作，如果它意识到确实如此，就会选择背叛以吃掉更多分数。

<p>“背刺”</p>

</div>

<div v-click="4">

## JOSS

通常重复对手的上一次行动，但同时有 10% 的概率偷偷背叛。

<p>“小动作”</p>

</div>

<div v-click="5">

## GRASSKAMP

重复对手的上一次行动，但总是在第 50 回合选择背叛并观察对手的反应。

<p>“试探”</p>

</div>

</div>

<p v-click="6" class="text-center">……</p>

---
hideInToc: true
---

# 简化版

<script lang="ts" setup>
import { RText } from 'roughness'
</script>

<style>
:deep(li p) {
  margin: 0.25em 0;
}
</style>

<div class="grid grid-cols-2 gap-4">

<div v-click>

## 一根筋派

- 永远合作

- 永远背叛

</div>

<div v-click>

## 两根筋派

- 偶尔合作 <RText type="comment">（背叛-背叛-合作-…）</RText>

- 偶尔背叛 <RText type="comment">（合作-背叛-背叛-…）</RText>

- 五五开 <RText type="comment">（合作-背叛-…）</RText>

- 随机 <RText type="comment">（50%-50%）</RText>

</div>

<div v-click>

## 应变派

- 以牙还牙 <RText type="comment">（合作，之后重复对手）</RText>

- 不信任 <RText type="comment">（背叛，之后重复对手）</RText>

- 宽容 <RText type="comment">（合作，除非对手连续两次背叛）</RText>

- 难哄 <RText type="comment">（合作，除非对手前两次中背叛过）</RText>

- 迟钝 <RText type="comment">（合作，但重复对手连续两次的选择）</RText>

</div>

<div v-click>

## 理解派

- 记仇 <RText type="comment">（合作，一旦对手背叛就永远背叛）</RText>

- 巴甫洛夫 <RText type="comment">（如果上次和对手选择一致，则合作，否则背叛）</RText>

- 常觉亏欠 <RText type="comment">（如果对手合作次数≥背叛次数，则合作，否则背叛）</RText>

- 公平自私 <RText type="comment">（如果对手合作次数>背叛次数，则合作，否则背叛）</RText>

</div>

</div>

---
layout: iframe
url: https://codepen.io/ooxx/embed/OJGjrzd?default-tab=js%2Cresult
---

---
hideInToc: true
layout: statement
---

# 如果加入更复杂的策略呢？

<v-click>

以牙还牙（Tit For Tat）：不好意思，还是我 (´. .̫ .`)

</v-click>

---
level: 2
layout: two-cols-header
---

<script lang="ts" setup>
import { RText } from 'roughness'
</script>

<style>
.slidev-layout {
  grid-template-rows: none !important;
}
</style>

# 为什么？

<v-clicks>

- 好人 VS 坏人

</v-clicks>

<br>

<v-clicks>

- 好人：【以牙还牙】、【记仇】

  - 倾向于通过合作拿分，不会主动选择背叛 <RText type="success" v-click="4">双赢！</RText>

- 坏人：【偶尔背叛】、JOSS

  - 倾向于通过背叛拿分，会尽可能主动打破持久的合作 <RText type="error" v-click="4">双输…</RText>

</v-clicks>

<br>

<v-click>

好人完胜！

</v-click>

---
hideInToc: true
level: 2
layout: two-cols-header
---

<style>
.slidev-layout {
  grid-template-rows: none !important;
}
</style>

# 为什么？

- 好人 VS 坏人

<v-clicks>

- 以牙还牙 VS 其他好人

</v-clicks>

::left::

<v-click>

<img src="/tft-vs-mistrust.png" alt="以牙还牙 VS 不信任" class="h-60">

以牙还牙 VS 不信任

</v-click>

::right::

<v-click>

<img src="/spiteful-vs-mistrust.png" alt="记仇 VS 不信任" class="h-60">

记仇 VS 不信任

</v-click>

---
level: 2
---

<script lang="ts" setup>
import { RText } from 'roughness'
</script>

# 关键特性

《合作的进化》罗伯特·阿克塞尔罗德

<v-clicks>

- 好人策略 <RText type="comment">（意味着更倾向于选择双赢）</RText>

- 谅解 <RText type="comment">（意味着在惩罚了背叛行为后依然优先选择合作）</RText>

- 及时报复 <RText type="comment">（意味着能够通过背叛抵消对手的背叛优势）</RText>

- 清晰 <RText type="comment">（意味着能够与其他策略建立稳定的关系）</RText>

</v-clicks>

---
hideInToc: true
layout: center
class: text-center
---

# 进化开始！

<video src="/evolution.mp4" class="h-60" controls></video>

---
hideInToc: true
---

<script lang="ts" setup>
import { RText } from 'roughness'
</script>

# 日常的“以牙还牙”

<v-clicks :depth="2">

- [`setPolling`](https://code.byted.org/ad/byted-star-libraries/blob/master/packages/shared-utils/src/lib/timer.ts)

  - 好人策略 <RText type="comment">（默认最短间隔轮询）</RText>

  - 谅解 <RText type="comment">（有效返回 -> 减少轮询间隔）</RText>

  - 及时报复 <RText type="comment">（无效返回 -> 延长轮询间隔）</RText>

  - 清晰

</v-clicks>

<br>

<v-clicks :depth="2">

- 研发 VS 产品

  - …

</v-clicks>

---
title: 总结
class: 'flex flex-col items-center'
---

# 谈谈博弈论

如何在重复的博弈中获胜

<Toc maxDepth="1" />

<style>
:deep(.router-link-exact-active) {
  color: var(--slidev-theme-primary);
  font-weight: bold;
}
</style>

---
hideInToc: true
---

# 心灵鸡汤

<script lang="ts" setup>
import { RText } from 'roughness'
</script>

<v-clicks>

- 充分的沟通 <RText type="comment">（打破囚徒困境）</RText>

- 构造利益关系 <RText type="comment">（避免公地悲剧）</RText>

- 善意假设、多元兼容和坦诚清晰 <RText type="comment">（赢得重复博弈）</RText>

</v-clicks>

---

# 扩展阅读

- [The Evolution of Trust](https://dccxi.com/trust/) 一个关于重复博弈的小游戏

- [囚徒困境所揭示的人生哲理](https://www.bilibili.com/video/BV19T4m1U7qX/) 真理元素制作的重复博弈介绍视频

- [*The Evolution of Cooperation*](https://bert.stuy.edu/pbrooks/spring2015/materials/HumanReasoning-2/Axelrod_Robert_The_Evolution_of_Cooperation.pdf) 《合作的进化》原书

---
hideInToc: true
layout: statement
---

# 谢谢！

<br>

全文参阅 [《谈谈博弈论：如何在重复的博弈中获胜》](https://bytedance.larkoffice.com/docx/Fs90dE0KOoUf1lx0uFScc0EYnJQ)

---
routeAlias: pirate-game
hideInToc: true
---

# 海盗分金币

有 5 个海盗抢到了 100 枚金币，他们决定从大当家开始每个人提出一个分配方案并投票，且提出人本人有 1.5 票；如果方案表决通过则按照方案执行，否则，提出方案的人就被扔下去喂鲨鱼。每个人的目的都是自己能拿更多的钱，在此基础上也希望能杀更多的人（这都什么团伙）。问最后大家分别能拿到几枚金币？
