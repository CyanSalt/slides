---
titleTemplate: '%s - CyanSalt'
author: CyanSalt
keywords: Game Theory

transition: slide-left
mdc: true
fonts:
  sans: 'Xiaolai SC'
  mono: 'Xiaolai SC'

hideInToc: true
class: text-center
---

# 谈谈博弈论

如何在重复的博弈中获胜

<script lang="ts" setup>
import { ArrowRight, Github, PencilLine } from 'lucide'
import { RButton, RIcon, RLink, RSpace } from 'roughness'
</script>

<RButton @click="$slidev.nav.next">
  <RSpace align="center">
    <slot>开始</slot>
    <RIcon :icon="ArrowRight" />
  </RSpace>
</RButton>

<RSpace class="abs-br m-6">
  <RLink @click="$slidev.nav.openInEditor()">
    <RIcon :icon="PencilLine" />
  </RLink>
  <RLink href="https://github.com/CyanSalt/slides/blob/main/slides.md?plain=1" target="_blank">
    <RIcon :icon="Github" />
  </RLink>
</RSpace>

<!--

首先要说的是，文章的内容并不是什么冷门知识；相反网络上有很多描述相似内容的文章。只是希望帮助未曾接触过博弈论的同学开一个小小的头。

-->

---
hideInToc: true
class: 'flex flex-col items-center'
---

# 谈谈博弈论

如何在重复的博弈中获胜

<Toc maxDepth="1" />

<br>

全文参阅 [《谈谈博弈论：如何在重复的博弈中获胜》](https://bytedance.larkoffice.com/docx/Fs90dE0KOoUf1lx0uFScc0EYnJQ)

<!--

大致按照如下结构，递进地讲解博弈论中比较经典的重复博弈问题。

在开始之前，先聊一下，为什么建议大家尝试了解博弈论。

-->

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

<!--

每一个计算机与软件行业的人都可以尝试了解博弈论。

我们现在能够通过软件控制计算机、完成一项工作，甚至于创造人工智能这样的复杂结构，都得益于 20 世纪 40 年代的“曼哈顿计划”——没错，就是一段时间前很流行的电影《奥本海默》中讲述的原子弹工程所在的项目。为了支持曼哈顿计划中的大量运算，科学家们开始使用计算机来完成计算工作。然而，那时的计算机程序全靠电子管等硬件结构完成，直到一位科学家指出，程序本身也可以是数据，可以使用计算机来存储，可以作为硬件输入的一部分。这就是软件的由来。

现在我们知道，这种思想，或者说实现计算机程序的方式，被称为冯·诺伊曼结构。那位科学家也就是冯·诺伊曼。

为什么要讲这段小故事呢？因为冯·诺伊曼还有一个头衔，那就是“博弈论之父”。而使他获得这一头衔的作品甚至早于冯·诺伊曼结构本身。

-->

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

<!--

首先探讨一下，什么是博弈论？

在英文中是 Game Theory，其实就是玩游戏的理论。1928 年冯·诺伊曼在他的论文《论客厅游戏理论》中最早阐述了一系列博弈论基本原理。

其实在中文里也是一样的，一般像这种词都是日本学者翻译的。“博弈”应该出自《论语》。

-->

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

<!--

> 子曰：“饱食终日，无所用心，难矣哉！不有博弈者乎，为之犹贤乎已。”

“博”的意思就是掷骰子，“弈”则是指围棋。这句话意思就是：

> 孔子说呀，“每天吃饱了啥也不干，让人难蚌！不是可以掷色子下围棋啥的吗，也比啥也不干强吧。”

（别骂了）

所以“博弈”的翻译非常精妙，即表示了博弈论来自于 Game，又把它具有一定的赌注、分析、决策的特性表现了出来。

-->

---
hideInToc: true
layout: statement
---

# 博弈论

一种探究<span v-mark.orange>在竞争关系中争取利益的策略</span>的学科。

<!--

通俗来说，博弈论是一种探究在竞争关系中争取利益的策略的学科（我自己概括的，不代表学界定义）。

我们玩游戏，例如简单的石头剪刀布，乃至更复杂的 LOL、王者荣耀，都会出现博弈论的身影。

一个经典的例子是：

-->

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

<!--

给不玩游戏的同学解释下，闪现是 MOBA 类游戏中进行一次快速位移的战略性技能，通常具有很长的冷却时间。在前期对抗时，如果发生了冲突，对手抵抗不过使用了【闪现】逃离，那么通常的潜规则就是不再去追击了。

乍一看很没有道理对吧？明明交闪已经说明对手尽显败势了，甚至闪现进入冷却也意味着他的能力进一步下降，为什么反而不追了呢？其实这和孙子兵法中描述的那句一样——

这其实就是所谓的“动态博弈”：你的对手做出了这样的决策，你要如何做才能让自己利益最大化？

对手很虚弱，还交了技能，但是同时也意味着我们更难以追上对手，追上对手的过程也要面临更大的风险，不仅会影响自己在接下来的节奏，更有可能被反杀……

尽管大多数时候我们并不会用到博弈论的一些结论，但也有时它能帮助我们进行决策。

这里需要大家思考的一个问题是：

-->

---
hideInToc: true
layout: statement
---

## 博弈 === 竞争 ？

<!--

博弈是否总是意味着“竞争”呢？

狭义的答案可能是“是”，但竞争中的合作可能也是一种常态。例如秉持不同理念的决策者之间互有竞争，但通常也有相同的目标。

-->

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

<!--

说到博弈论总是绕不开的一个话题就是“囚徒困境”。假设你不知道什么是囚徒困境（感觉可能性不高），或者是忘记了，我们来一起回顾一下：

-->

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

<!--

从前有一天，有一个银行被劫匪洗劫了。警察通过蛛丝马迹找到了嫌疑人，你 和 老六（你也不知道老六是谁，当然我们也不知道究竟是不是你或者老六干的）；然而，警察并没有足够的证据证明案件是这俩人干的。

鉴于**你们互相不认识，没有共同的利益**（这很关键）……

-->

---

<div class="h-full flex flex-col justify-center items-center">
  <img class="h-60" src="/prisoners-2.png" alt="Prisoners">
</div>

<!--

警察决定把你们两人分开审讯。

警察对你说：

- 你可以选择沉默，或者是指认老六

- 抢劫罪一旦成立会被判 10 年

- 如果指认后发现你们是共犯，会被分别判 5 年

同时律师告诉你：

- 假设你和老六都没有指认对方，你俩都只用拘留 251 天就完事儿了

另一边，警察和律师也对老六说了相同的话。

-->

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

<!--

我来帮你推理一下：我们先考虑一下老六会不会招：

- 假设老六指认了你：那如果你指认他，你是 5 年；如果你不指认，你就是 10 年

- 假设老六没指认你：那如果你指认他，你是无罪；如果你不指认，你就是 251 天

所以考虑两种情况，不管老六有没有指认你，你都应该指认她，这样才能让自己利益最大化。

OK 决定了。所以有什么问题呢？

——问题就在于，老六也是这么想的，于是最终你俩都被判 5 年，警察的目的达到了；而本来对你们来说，最好的结果应该是都领 251 天就够了。

博弈论中把囚徒困境面临的情况叫作**非零和博弈**，意思是并不是有人赚就有人亏，大家有可能一起赚或者一起亏；相反诸如股市就更像是零和博弈，~~不论大家怎么决策都是一起亏~~。

你和老六最终被判 5 年的结果称为纳什均衡。

-->

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

<!--

之所以叫纳什均衡，是因为它来自于纳什。

美国数学家、《美丽心灵》的主角约翰·福布斯·纳什的名字命名。他不是男爵。

简单来说，纳什均衡就是在一场非零和博弈中，每个人都让自己利益最大化的结果。纳什利用角谷不动点定理证明了纳什均衡是必然存在的，但显然，纳什均衡很多时候都不会得到最好的结果。

-->

---
hideInToc: true
layout: statement
---

# 均衡 !== 整体最优

（甚至不是局部最优）

<!--

就像上面的例子一样。假设一人犯罪的结果是被判 5 年零 1 天，也不会影响你和老六的选择。在这种情况下，纳什均衡基本上就是纯纯的双输。

扩展聊下，可能有很多人也了解一个概念叫“帕累托最优”。

-->

---
level: 2
layout: center
class: text-center
---

# 帕累托最优

<img v-click class="h-60" src="/pareto-optimality.png" alt="Pareto Optimality">

<!--

它和纳什均衡很相似，意思是没有办法在不损伤其他人的利益的情况下让任何人获益。

> 比如我和马云人均 300 亿美元，假如马云给我 9999 万美元，我们俩就都是亿万富翁了，但是这么干马云亏了，所以他不可能给我，因此我们现在的状态就是帕累托最优。

帕累托最优导致了帕累托分布的产生，也就是 20% 的富人占据了 80% 的财富而没有带动后富，因为带动后富也是会损伤他们的利益的。

囚徒困境的纳什均衡显然不是帕累托最优，因为大家都合作的结果对每个人都要优于大家都背叛。这似乎很像是机器学习的梯度下降算法中容易求得一个局部最小值，但这个值不一定是全局最小的。

大家可以再仔细想想，是什么让囚徒困境中的两人无法取得全局最优的结果呢？

-->

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

<!--

刚才提到的关键问题：警察会把你和老六分开审讯。这意味着你们因为无法得知对方的想法，从而无法达成合作。

除此之外呢？

另一个原因我可以用一个其他的例子来解释。

-->

---
level: 2
layout: center
class: text-center
transition: slide-right
---

# 公地悲剧

<img v-click class="h-60" src="/tragedy-of-the-commons.jpg" alt="Tragedy of the Commons">

<!--

公地悲剧，简单地说就是，如果一片牧场里只有一个牧羊人，他会控制羊的数量以使得增加羊带来的收益=增加羊带来的牧场损耗；然而如果是有两个牧羊人，牧场损耗带来的成本被分摊，但是增加羊的收益还是独享的，因此两个牧羊人都会倾向于增加更多羊的数量，从而使牧场超负荷直至荒芜。

另一个例子是，大家决定一起出去 AA 下馆子，每个人都可以选择点便宜的或者贵的，由于点贵的成本被大家分摊了，所以大家都倾向于点贵的菜。这有时候也被称为“用餐者困境”。

“三个和尚没水吃”的故事一定程度上也和它相关。

-->

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

<!--

从公地悲剧我们也能发现，因为你和老六之间没有利益关系，因此对方被判刑这件事实际上变成了公地的一部分。

-->

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

<!--

回到刚才的场景，如果是这样的话，怎样才能让你和老六在博弈中不要双输呢？

-->

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

<!--

中国有句古话叫~~闷声发大财~~吃一堑长一智，所以如果我们能够一直博弈下去，是不是就能够推测出对方究竟是 24K 纯坏比，还是和我一样善良纯真勇敢的人呢？换言之，**如果这场博弈重复进行，我们又要用怎样的策略让自己利益最大化呢？**

这就是在预习时我们玩的这个游戏。回顾一下，这个游戏和囚徒困境的表格或者说矩阵具有类似的结构：

-->

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

<!--

合作 -> 共赢

背叛 -> 赢得更多

相互背叛 -> 双输

按照囚徒困境的策略，不论对手如何选择，我们选择“背叛”在单次游戏中总是对自己最有利的，也就是会达到纳什均衡；然而事情并没有这么简单：

-->

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

<!--

- 博弈论的结论表明，在重复博弈中存在多重均衡，也就是说不止有一种纳什均衡的状态；

- 作为上述结论的一项依据，我们可能需要注意的是：游戏有不止两位玩家，因此，其他玩家之间进行的游戏也会对结果造成影响

还需要注意到的一个关键信息是，选手是不知道每轮比赛进行的场次的。否则，按照单次囚徒困境的纳什均衡，在最后一次比赛中我们总应该选择背叛；进一步思考，因为大家都会这么想，意味着对手最后一轮也会背叛，所以倒数第二次我们也应该选择背叛……以此类推，最终的策略变成了总是背叛，但这显然与我们本来想要研究的方向背道而驰。

-->

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

<!--

1980 年代，美国政治学家阿克塞尔罗德教授邀请了 14 个不同领域的专家进行了这个游戏，或者说比赛（与我们不同的是，当时比赛使用的语言是 Basic），这些专家包含数学家、经济学家、政治学家、心理学家等多个领域。

阿克塞尔罗德教授和我一样，给出了一个示例程序 SAMPLE：

-->

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

<!--

> 示例：默认合作，如果对手连续两次背叛，则下一次也会背叛

看上去听合理的，我给他的代号是“宽容”。

本次比赛的其他参赛选手包括了很多复杂策略，例如：

- 程序 DOWNING 试图测试对手是否总是倾向于合作，如果它意识到确实如此，就会选择背叛以吃掉更多分数

- 程序 JOSS 通常重复对手的上一次行动，但同时有 10% 的概率偷偷背叛

- 程序 GRASSKAMP 也重复对手的上一次行动，但他总是在第 50 回合选择背叛并观察对手的反应

- ……

为了简化这一流程，我参考了一些其他尝试重复实验的文章，实现了一些最简单的策略。

-->

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

<!--

主要分为以下几类：

- 一根筋派（永远只选择一种行为）

- 两根筋派（不管对手如何选择，总是按照自己的想法执行）

- 应变派（根据对手的选择给出不同的反应）

- 理解派（尝试理解对手的策略）

现在，让我们猜猜看：在简化版的游戏中，谁会获得最终的胜利？

-->

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

<!--

答案是，不论在哪些策略群体内，最终得分最高的总是那个看上去足够简单的策略：【以牙还牙】；甚至，它在应对那些复杂策略时表现出了更明显的优势！

但是，为什么？

-->

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

<!--

我们可以尝试将这些策略分成两类：

- “好人”：他们更倾向于通过合作拿分，不会主动选择背叛。像【以牙还牙】、【记仇】都属于此类

- “坏人”：他们更倾向于通过背叛拿分，会尽可能主动打破持久的合作。像【偶尔背叛】，乃至于 DOWNING 和 JOSS 都属于此类

回顾一下对游戏特征的描述，我们会发现，好人的胜利几乎是必然的：尽管好人和坏人进行游戏时是不利的，但是，好人还会与好人进行游戏，此时是双赢的；反之，坏人和坏人则是双输的。因此，好人更有机会获得更高分数，尽管在单次比赛中可能会输给坏人。

事实上，在原始游戏的 15 种复杂的策略中（当然也包含了【以牙还牙】），8 种好人策略占据了总分数的前八名。

-->

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

<!--

【以牙还牙】在众多好人中如何脱颖而出？我们尝试对比一下它和好人里表现最差的【记仇】，我们考虑一种比较简单的场景：以牙还牙和记仇分别于比较简单的坏人【不信任】进行游戏：

- 由于【以牙还牙】和【不信任】在第一步时失之交臂，因此他们开始交替进行对对方的惩罚……

- 【不信任】在第一步的选择导致了【记仇】和它的双输……

此外，我们也很容易想到，绝对的好人实际上是没有优势的，例如我们可以对比【以牙还牙】和【永远合作】。就像预习时举的例子一样，【永远合作】将被【五五开】在一半的回合数中吃掉分数，而【以牙还牙】则能够像和【不信任】游戏时一样，与【五五开】交替进行惩罚。

另一个问题是：【以牙还牙】总是最有效的吗？事实上，我们可以控制参加比赛的策略，例如让坏人占据多数；在这种情况下，原本处于劣势的【记仇】表现将可能会好于【以牙还牙】，因为它能够更进一步避免被恶意占便宜。对我们来说，这里更重要的结论是：

事实上并不存在一个总是有效的重复博弈策略，策略的好坏会受到参与博弈的其他策略的影响。

-->

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

<!--

这个游戏是否具有现实意义呢？事实上，发明这个游戏的 Rand 公司主要做的就是冷战时期的国际政治分析，我们可以看到，不同策略的比赛实际上和我们看到的国际政治非常相似：

- 美国：制裁俄罗斯

- 俄罗斯：拒绝美元结算

- 美国：炸了你丫的管道

- ……

我们能否从【以牙还牙】与众多策略的博弈中的获胜中获取一些经验呢？阿克塞尔罗德教授在《合作的进化》中给出了答案：即使是在游戏规则进行有限调整的情况下（例如修改得分、比赛轮次等），获胜的策略总是满足：

- 好人策略，意味着更倾向于选择双赢

- 谅解，意味着在惩罚了背叛行为后依然优先选择合作

- 及时报复，意味着能够通过背叛抵消对手的背叛优势

- 清晰，意味着能够与其他策略建立稳定的关系

这些特性实际上是缺一不可的。比方说，有时候重复博弈会被运用在一种进化游戏中，也就是在上面的游戏基础上，每种策略初始不止有一个玩家，但会在一轮循环赛之后淘汰掉分数最低的几名玩家，同时复制等量的分数最高的玩家。

在这种情况下，会发生什么样的事呢？

-->

---
hideInToc: true
layout: center
class: text-center
---

# 进化开始！

<video src="/evolution.mp4" class="h-60" controls></video>

<!--

——结果是，坏人会迅速把滥好人，也就是不会及时报复的玩家淘汰，然后坏人被抱团共赢的以牙还牙们慢慢消灭。如果我们把我们的世界想象得更加残酷一些，那么显然，做一个以牙还牙的好人要好过做一个坏人，更要好过做一个永远的好人。这或许就是《论语》中所讲的：

> 或曰：“以德报怨，何如？”子曰：“何以报德？以直报怨，以德报德。”

-->

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

<!--

此外，这些条件可以是更加广义的。一个例子是星图前端的轮询使用的 setPolling 函数，它实际上就是一种【以牙还牙】的算法（当然准确地说，它更接近于【宽容】算法）：

- 它优先选择合作（默认采用最短的轮询间隔）

- 它会尝试从背叛转向合作（在有效返回时，减少轮询间隔）

- 它会用背叛来惩罚背叛（在无效返回时，延长轮询间隔）

- 它的行为可以预测

常见的 TCP 拥塞控制算法等也采用了相似的逻辑，我们现在就可以从博弈论的角度获悉这是一种比较理想的方式。

再举个实际工作中的例子：

> 这个女人叫小帅，这个男人叫小美，这个年轻人叫老王，他们都是工程师；他们都在绩效评估中和 Leader 反馈了产品经理大壮的问题；

> 小帅认为大壮产出低，Leader 了解后发现是因为小帅总是拒绝或者拖延大壮提的需求；

> 小美给大壮的 360 评估打了 F，因为两年前大壮的 PRD 漏了一个埋点字段，从此之后小美再也没接过大壮的需求；

> 老王抱怨大壮总是给他插入需求，就因为半年前大壮的一个不紧急的需求老王给他敏捷支持了

看，即使是在充满了合作的场景中，坚持博弈的基本原则也是有效的，甚至在多数情况下这能为我们带来最好的结果。

-->

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

<!--

回顾囚徒困境和重复博弈两个例子，我们会发现一些心灵鸡汤，也就是本文《如何在重复的博弈中获胜》的答案：

- 充分的沟通（打破囚徒困境）

- 构造利益关系（避免公地悲剧）

- 善意假设、多元兼容和坦诚清晰（赢得重复博弈）

合作，看起来相比选择自私会处于劣势，我们似乎没有理由选择和非亲非故的同事合作；但是，我们为同一个目标一齐努力，在彼此合作之中创造新的价值，而不是在零和博弈中拼个你死我活；这注定了我们能够合作，最终也会合作。我们通过合作释放的善意，最终成为了我们所处的善意环境本身。

所以，如果再玩一次预习的游戏，你会给出怎样的策略呢？

-->

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

<script lang="ts" setup>
import { Github } from 'lucide'
import type { RoughSVG } from 'roughjs/bin/svg'
import { RGraphics, RIcon, RLink } from 'roughness'

function drawSlidev(rc: RoughSVG, svg: SVGSVGElement) {
  const square = rc.rectangle(14, 14, 90, 90, {
    stroke: '#2988B1',
    fill: '#3ACBD4',
  })
  svg.appendChild(square)
  const circle = rc.circle(45, 45, 90, {
    stroke: '#3AB9D5',
    fill: '#95F0CF',
  })
  svg.appendChild(circle)
  const triangle = rc.path('M56.127 63.925C54.9501 59.5327 54.3617 57.3366 54.9439 55.8199C55.4517 54.497 56.497 53.4517 57.8199 52.9439C59.3366 52.3617 61.5327 52.9501 65.925 54.127L87.7563 59.9767C92.1485 61.1536 94.3446 61.742 95.367 63.0046C96.2588 64.1058 96.6414 65.5338 96.4197 66.9334C96.1656 68.5379 94.5579 70.1456 91.3426 73.3609L75.3609 89.3426C72.1456 92.5579 70.5379 94.1656 68.9333 94.4197C67.5337 94.6414 66.1058 94.2588 65.0046 93.367C63.742 92.3446 63.1536 90.1485 61.9767 85.7563L56.127 63.925Z', {
    stroke: '#FFA800',
    fill: '#FFEB83',
  })
  svg.appendChild(triangle)
}

function drawVercel(rc: RoughSVG, svg: SVGSVGElement) {
  const path = rc.path('M8 1L16 15H0L8 1Z', {
    stroke: 'currentColor',
    fill: 'currentColor',
  })
  svg.appendChild(path)
}
</script>

<br>

全文参阅 [《谈谈博弈论：如何在重复的博弈中获胜》](https://bytedance.larkoffice.com/docx/Fs90dE0KOoUf1lx0uFScc0EYnJQ)

<br>
<br>

<style>
.powered-by a {
  border-bottom: none;
}
.powered-by a:hover {
  color: inherit;
}
</style>

<div class="powered-by mx-auto flex gap-4 items-center w-1/4">

<a class="flex-1" href="https://roughness.vercel.app/" target="_blank">
<LightOrDark>
  <template #dark>
  <p class="mx-auto w-2/5">

  ![Roughness](https://roughness.vercel.app/r-dark.svg)

  </p>
  </template>
  <template #light>
  <p class="mx-auto w-2/5">

  ![Roughness](https://roughness.vercel.app/r.svg)

  </p>
  </template>
</LightOrDark>
</a>

<a class="flex-1" href="https://sli.dev/" target="_blank">
<p class="mx-auto w-4/5">

![Slidev](https://raw.githubusercontent.com/slidevjs/slidev/179a313fad91d952eddc33cb0c0bfb00f1a4474c/assets/logo.svg)

</p>
</a>

<a class="flex-1 leading-none text-sm" href="https://github.com/lxgw/kose-font/" target="_blank">
小赖<br>字体
</a>

<a class="flex-1" href="https://vercel.com/" target="_blank">
<svg class="mx-auto w-1/2" viewBox="0 0 76 65" fill="none" xmlns="http://www.w3.org/2000/svg">
  <path d="M37.5274 0L75.0548 65H0L37.5274 0Z" fill="currentColor"/>
</svg>
</a>

</div>

<br>

<RLink href="https://github.com/CyanSalt/slides/blob/main/slides.md?plain=1" target="_blank">
  <RIcon :icon="Github" />
</RLink>

---
routeAlias: pirate-game
hideInToc: true
---

# 海盗分金币

有 5 个海盗抢到了 100 枚金币，他们决定从大当家开始每个人提出一个分配方案并投票，且提出人本人有 1.5 票；如果方案表决通过则按照方案执行，否则，提出方案的人就被扔下去喂鲨鱼。每个人的目的都是自己能拿更多的钱，在此基础上也希望能杀更多的人（这都什么团伙）。问最后大家分别能拿到几枚金币？
