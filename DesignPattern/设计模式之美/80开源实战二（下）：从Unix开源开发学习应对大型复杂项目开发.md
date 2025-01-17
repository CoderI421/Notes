# 80开源实战二（下）：从Unix开源开发学习应对大型复杂项目开发

> 2020-05-06 王争
>
> 设计模式之美 进入课程 

![](media/image3.png)

> 上两节课，我们分别从代码编写、研发管理的角度，学习了如何应对大型复杂软件开发。在
>
> ![](media/image9.png)研发管理这一部分，我们又讲到比较重要的几点，它们分别是编码规范、单元测试、持续重构和 Code Review。其中，前三点在专栏的理论部分都有比较详细的讲解，而唯独 Code
>
> Review 我们还没有讲过，所以，今天我就借机会和你补充一下这一部分的内容。



> 很多年前，我跟一个有十几年研发经验的某一线大厂的技术专家聊天，聊天中我提起了Code Review，他便对 Code Review 一顿否定。他说，Code Review 比较浪费时间，往
>
> 往会虎头蛇尾，不可能在企业中很好地落地执行。当我又提起，Code Review 在 Google 执行得很好，并且是已经习以为常的开发流程的时候，他竟然说这绝对不可能。
>
> 一个技术不错，可以玩转各种架构、框架、中间件的资深 IT 从业者，居然对 Code Review 有如此的偏见，这到底是哪里出了问题呢？我觉得问题主要还是出自认知上。
>
> 所以，今天，我并不打算讲关于如何做 Code Review 的方法论，我更希望充当一个 Code Review 布道师的角色，讲一讲为什么要进行 Code Review，Code Review 的价值在哪
>
> 里，让你重视、认可 Code Review。因为我觉得，只要从认知上接受了 Code Review，对于高智商的 IT 人群来说，搞清楚如何做 Code Review 并不是件难事。而且，Google 也开源了它自己的 Code Review 最佳实践，网上很容易搜到，你完全可以对照着来做。
>
> 话不多说，让我们正式开始今天的内容吧！

# 我为什么如此强调 Code Review？

> Code Review 中文叫代码审查。据我了解，在国内绝大部分的互联网企业里面，很少有将Code Review 执行得很好的，这其中包括 BAT 这些大厂。特别是在一些需求变动大、项目工期紧的业务开发部门，就更不可能有 Code Review 流程了。代码写完之后随手就提交上去，然后丢给测试狠命测，发现 bug 再修改。
>
> 相反，一些外企非常重视 Code Review，特别是 FLAG 这些大厂，Code Review 落地执 行得非常好。在 Google 工作的几年里，我也切实体会到了 Code Review 的好处。这里我就结合我自身的真实感受讲一讲 Code Review 的价值，试着“说服”一下你。

## Code Review 践行“三人行必有我师”

> 有时候你可能会觉得，团队中的资深员工或者技术 leader 的技术比较牛，写的代码很好， 他们的代码就不需要 Review 了，我们重点 Review 资历浅的员工的代码就可以了。实际上，这种认识是不对的。
>
> 我们都知道，Google 工程师的平均研发水平都很高，但即便如此，我们发现，不管谁提交的代码，包括 Jeff Dean 的，只要需要 Review，都会收到很多 comments（修改意
>
> 见）。中国有句老话，“三人行必有我师”，我觉得用在这里非常合适。即便自己觉得写得已经很好的代码，只要经过不停地推敲，都有持续改进的空间。
>
> 所以，永远不要觉得自己很厉害，写的代码就不需要别人 Review 了；永远不要觉得自己水平很一般，就没有资格给别人 Review 了；更不要觉得技术大牛让你 Review 代码只是缺少你的一个“approve”，随便看看就可以。

## Code Review 能摒弃“个人英雄主义”

> 在一个成熟的公司里，所有的架构设计、实现，都应该是一个团队的产出。尽管这个过程可能会由某个人来主导，但应该是整个团队共同智慧的结晶。
>
> 如果一个人默默地写代码提交，不经过团队的 Review，这样的代码蕴含的是一个人的智
>
> 慧。代码的质量完全依赖于这个人的技术水平。这就会导致代码质量参差不齐。如果经过团队多人 Review、打磨，代码蕴含的是整个团队的智慧，可以保证代码按照团队中的最高水准输出。

## Code Review 能有效提高代码可读性

> 前面我们反复强调，在大部分情况下，代码的可读性比任何其他方面（比如扩展性等）都重要。可读性好，代表后期维护成本低，线上 bug 容易排查，新人容易熟悉代码，老人离职时代码容易接手。而且，可读性好，也说明代码足够简单，出错可能性小、bug 少。
>
> 不过，自己看自己写的代码，总是会觉得很易读，但换另外一个人来读你的代码，他可能就不这么认为了。毕竟自己写的代码，其中涉及的业务、技术自己很熟悉，别人不一定会熟 悉。既然自己对可读性的判断很容易出现错觉，那 Code Review 就是一种考察代码可读性的很好手段。如果代码审查者很费劲才能看懂你写的代码，那就说明代码的可读性有待提高了。
>
> 还有，不知道你有没有这样的感受，写代码的时候，时间一长，改动的文件一多，就感觉晕乎乎的，脑子不清醒，逻辑不清晰？有句话讲，“旁观者清，当局者迷”，说的就是这个意思。Code Review 能有效地解决“当局者迷”的问题。在正式开始 Code Review 之前， 当我们将代码提交到 Review Board（Code Review 的工具界面）之后，所有的代码改动 都放到了一块，看起来一目了然、清晰可见。这个时候，还没有等其他同事 Review，我们自己就能发现很多问题。

## Code Review 是技术传帮带的有效途径

> 良好的团队需要技术和业务的“传帮带”，那如何来做“传帮带”呢？当然，业务上面，我们可能通过文档或口口相传的方式，那技术呢？如何培养初级工程师的技术能力呢？Code Review 就是一种很好的途径。每次 Code Review 都是一次真实案例的讲解。通过 Code Review，在实践中将技术传递给初级工程师，比让他们自己学习、自己摸索来得更高效！

## Code Review 保证代码不止一个人熟悉

> 如果一段代码只有一个人熟悉，如果这个同事休假了或离职了，代码交接起来就比较费劲。有时候，我们单纯只看代码还看不大懂，又要跟 PM、业务团队、或者其他技术团队，再重复来一轮沟通，搞的其他团队的人都很烦。而 Code Review 能保证任何代码同时都至少有两个同事熟悉，互为备份，有备无患，除非两个同事同时都离职……

## Code Review 能打造良好的技术氛围

> 提交代码 Review 的人，希望自己写的代码足够优秀，毕竟被同事 Review 出很多问题，是件很丢人的事情。而做 Code review 的人，也希望自己尽可能地提出有建设性意见，展示自己的能力。所以，Code Review 还能增进技术交流，活跃技术氛围，培养大家的极客精神，以及对代码质量的追求。
>
> 一个良好的技术氛围，能让团队有很强的自驱力。不用技术 leader 反复强调代码质量有多重要，团队中的成员就会自己主动去关注代码质量的问题。这比制定各种规章制度、天天督促执行要更加有效。实际上，我多说一句，好的技术氛围也能降低团队的离职率。

## Code Review 是一种技术沟通方式

> Talk is cheap，show me the code。怎么“show”，通过 Code Review 工具
>
> 来“show”，这样也方便别人反馈意见。特别是对于跨不同办公室、跨时区的沟通， Code Review 是一种很好的沟通方式。我今天白天写的代码，明天来上班的时候，跨时区的同事已经帮我 Review 好了，我就可以改改提交，继续写新的代码了。这样的协作效率会很高。

## Code Review 能提高团队的自律性

> 在开发过程中，难免会有人不自律，存在侥幸心理：反正我写的代码也没人看，随便写写就提交了。Code Review 相当于一次代码直播，曝光 dirty code，有一定的威慑力。这样大家就不敢随便应付一下就提交代码了。

# 如何在团队中落地执行 Code Review？

> 刚刚讲了这么多 Code Review 的好处，我觉得大部分你应该都能认可，但我猜你可能会说，Google 之所以能很好地执行 Code Review，一方面是因为有经验的传承，起步阶段 已经过去了；另一方面是本身员工技术素质、水平就很高，那在一个技术水平没那么强的团队，在起步阶段或项目工期很紧的情况下，如何落地执行 Code Review 呢？
>
> 接下来，我就很多人关于 Code Review 的一些疑惑，谈谈我自己的看法。

### 有人认为，Code Review 流程太长，太浪费时间，特别是工期紧的时候，今天改的代码， 明天就要上，如果要等同事 Review，同事有可能没时间，这样就来不及。这个时候该怎么办呢？

> 我所经历的项目还没有一个因为工期紧，导致没有时间 Code Review 的。工期都是人排的，稍微排松点就行了啊。我觉得关键还是在于整个公司对 Code Review 的接受程度。而且，Code Review 熟练之后，并不需要花费太长的时间。尽管开始做 Code Review 的时候，你可能因为不熟练，需要有一个 checklist 对照着来做。起步阶段可能会比较耗时。但当你熟练之后，Code Review 就像键盘盲打一样，你已经忘记了哪个手指按的是哪个键
>
> 了，扫一遍代码就能揪出绝大部分问题。

### 有人认为，业务一直在变，今天写的代码明天可能就要再改，代码可能不会长期维护，写得太好也没用。这种情况下是不是就不需要 Code Review 了呢？

> 这种现象在游戏开发、一些早期的创业公司或者项目验证阶段比较常见。项目讲求短平快， 先验证产品，再优化技术。如果确实面对的还只是生存问题，代码质量确实不是首要的，特殊情况下，不做 Code Review 是支持的！
>
> 有人说，团队成员技术水平不高，过往也没有 Code Review 的经验，不知道 Review 什么，也 Review 不出什么。自己代码都没写明白，不知道什么样的代码是好的，什么样的代码是差的，更不要说 Review 别人的代码了。在 Code Review 的时候，团队成员大眼瞪小眼，只能 Review 点语法，形式大于效果。这种情况该怎么办？
>
> 这种情况也挺常见。不过没关系，团队的技术水平都是可以培养的。我们可以先让资深同 事、技术好的同事或技术 leader，来 Review 其他所有人的代码。Review 的过程本身就是一种“传帮带”的过程。慢慢地，整个团队就知道该如何 Review 了。虽然这可能会有一个
>
> 相当长的过程，但如果真的想在团队中执行 Code Review，这不失为一种“曲线救国”的方法。

### 还有人说，刚开始 Code Review 的时候，大家都还挺认真，但时间长了，大家觉得这事跟 KPI 无关，而且我还要看别人的代码，理解别人写的代码的业务，多浪费时间啊。慢慢地，Code Review 就变得流于形式了。有人提交了代码，随便抓个人 Review。Review 的人也不认真，随便扫一眼就点“approve”。这种情况该如何应对？

> 我的对策是这样的。首先，要明确的告诉 Code Review 的重要性，要严格执行，让大家不要懈怠，适当的时候可以“杀鸡儆猴”。其次，可以像 Google 一样，将 Code Review 间接地跟 KPI、升职等联系在一块，高级工程师有义务做 Code Review，就像有义务做技术面试一样。再次，想办法活跃团队的技术氛围，把 Code Review 作为一种展示自己技术的机会，带动起大家对 Code Review 的积极性，提高大家对 Code Review 的认同感。
>
> 最后，我再多说几句。Google 的 Code Review 是做得很好的，可以说是谷歌保持代码高质量最有效的手段之一了。Google 的 Code Review 非常严格，多一个空行，多一个空格，注释有拼错的单词，变量命名得不够好，都会被指出来要求修改。之所以如此吹毛求 疵，并非矫枉过正，而是要给大家传递一个信息：代码质量非常重要，一点都不能马虎。

# 重点回顾

> 好了，今天的内容到此就讲完了。我们一块来总结回顾一下，你需要重点掌握的内容。
>
> 今天，我们主要讲了为什么要做 Code Review，Code Review 的价值在哪里。我的总结如下：Code Review 践行“三人行必有我师”、能摒弃“个人英雄主义”、能有效提高代码可读性、是技术传帮带的有效途径、能保证代码不止一个人熟悉、能打造良好的技术氛围、是一种技术沟通方式、能提高团队的自律性。
>
> 除此之外，我还对 Code Review 在落地执行过程中的一些问题，做了简单的答疑。我这里就不再重复罗列了。如果你在 Code Review 过程中遇到同样的问题，希望我的建议对你有所帮助。

# 课堂讨论

> 对是否应该做 Code Review，你有什么看法呢？你所在的公司是否有严格的 Code Review 呢？在 Code Review 的过程中，你又遇到了哪些问题？
>
> 欢迎留言和我分享你的想法。如果有收获，也欢迎你把这篇文章分享给你的朋友。

![](media/image10.png)

> © 版权归极客邦科技所有，未经许可不得传播售卖。 页面已增加防盗追踪，如有侵权极客邦将依法追究其法律责任。
>
> 上一篇 79 \| 开源实战二（中）：从Unix开源开发学习应对大型复杂项目开发
>
> 下一篇 81 \| 开源实战三（上）：借Google Guava学习发现和开发通用功能模块
>
> ![](media/image11.png)**精选留言 (18)**
>
> ![](media/image13.png)**xindoo**
>
> 2020-05-06
>
> https://github.com/xindoo/eng-practices-cn 我们翻译的谷歌工程实践中文版，老师说的谷歌开源的code review就在这，欢迎查阅。
>
> 展开

![](media/image14.png)![](media/image15.png)11

> ![](media/image16.png)**天华**
>
> 2020-05-06
>
> 如果老师能把过去cr经验，需要注意的关键点整理出来就更好了

![](media/image17.png)![](media/image18.png)6

> ![](media/image19.png)**小喵喵**
>
> 2020-05-06
>
> 如果老师能讲解一些实战就更好了。多举例说明这段代码审查出什么问题以及如何修改。

![](media/image20.png)![](media/image18.png)1 4

> ![](media/image21.png)**小黑**
>
> 2020-05-06
>
> 能分享下review的checklist么
>
> 展开
>
> ![](media/image22.png)![](media/image23.png)3
>
> ![](media/image24.png)**+ +**
>
> 2020-05-06
>
> 所在公司非常重视code review 需要至少得到两个人的approved 分别是 业务组一个和架构组一个
>
> 刚来公司时的第一次代码提交 有20多个comments 现在也能给别人review了
>
> 展开
>
> ![](media/image22.png)![](media/image23.png)1
>
> ![](media/image25.png)**Jackey**
>
> 2020-05-06
>
> 团队现在的code review基本流于形式了，想要改善感觉也没什么太好的办法，太多人自由惯了…只能做好自己了
>
> 展开

![](media/image17.png)![](media/image18.png)1

> ![](media/image26.png)**，**
>
> 2020-05-07
>
> 目前所在的公司有code review的习惯,但是仅限于leader来review,而且并不严格,主要保证逻辑的正确和代码的可读性,我个人在来到公司之后看了代码整洁之道和effective java这两本书,感觉对写出整洁代码有一定的帮助
>
> 展开
>
> ![](media/image27.png)**will**
>
> 2020-05-07
>
> 还是很有必要进行review的，这个也是个学习的过程，可以学习别人的设计思想。

![](media/image28.png)![](media/image29.png)

> ![](media/image30.png)**Heaven**
>
> 2020-05-06
>
> Code Review是个好东西,懂得人不少,可是能够执行起来的难上加难,大厂何尝不是,好处能列一大堆,可是咱不是领导,没有带头的能力,自己一个人搞Code Review起不了什么作用,只能各扫门前雪,自己对自己的些重构罢了
>
> 展开

![](media/image31.png)![](media/image29.png)

> ![](media/image32.png)**jaryoung**
>
> 2020-05-06
>
> code review，个人觉得国内至少有一半的公司都没有，至少一半的一半是流于形式。che ck list：

1.  编码规范（借助工具，例如国内的p3c，还有就是借助checkstyle等工具）

2.  编码技巧（例如，提前终止错误），慢慢建立自己公司的知识库。最后，就是坚持坚持再坚持，教育教育再教育。

> 展开

![](media/image33.png)![](media/image34.png)

> ![](media/image35.png)**南山**
>
> 2020-05-06
>
> 公司在猛抓质量，cr也有足够的重视，自己的松懈也导致了质量的下降。
>
> 亲身经历一个功能的推倒重来到现在的大单体，大部分原因都是自己对重构、质量不够重视，后续反思，矫正，践行！！！
>
> 展开

![](media/image28.png)![](media/image29.png)

> ![](media/image36.png)**Frank**
>
> 2020-05-06
>
> Code Review 除了能对一些代码提出修改建议之外，个人觉得自己能从别人写的代码学到一些好的设计，好的思想。所以自己在平时任务完成的情况下，也会看看别人写的代码， 看看他是怎么实现的，如果自己来实现是否有更好的方式等。目前团队中有部分项目代码提交是需要 review 通过才能提交的，在这过程之中，code review 比较侧重的是代码规范，项目中一些特别注意的点，基本上不太可能去充分了解别人的完成的业务，主要是…
>
> 展开
>
> ![](media/image31.png) ![](media/image37.png)
>
> ![](media/image38.png)**荀麒睿**
>
> 2020-05-06
>
> 看了争哥这篇文章，想了下我们公司，发现就是没有code review的氛围，项目工期动不动就是今天要改完，明天领导就要看，代码也都是五花八门，有些临时写的代码后期也就得过且过，全都已经自由惯了。之前架构师还在推荐进行code review，但是还是很难执行。不过我个人认为，code review是有必要的，这样形成一个好的技术氛围，大家一起成长的感觉很是不错
>
> 展开

![](media/image28.png)![](media/image37.png)

> ![](media/image39.png)**do it**
>
> 2020-05-06
>
> 当前有的项目有CodeReview,不过基本都是检查下编码规范。

![](media/image40.png)![](media/image34.png)

> ![](media/image41.png)**守拙**
>
> 2020-05-06
>
> 课堂讨论:
>
> 个人对于Code Review的看法是正面的, CR能有效维持(maintain)项目代码可维护性, 提升团队凝聚力, 老师说良好的CR能降低团队离职率是不无道理的.
>
> …
>
> 展开

![](media/image40.png)![](media/image34.png)

> ![](media/image42.png)**小晏子**
>
> 2020-05-06
>
> 非常赞成code review，在我的平时工作中，code review非常严格，遇到的问题就是像文中提到的，一个特性开发好了之后要好长一段时间才能合入到主干分支，不过这个有个好处是上线bug确实很少，代码质量也比较高！
>
> 展开

![](media/image31.png)![](media/image37.png)

> ![](media/image43.png)**jinjunzhu**
>
> 2020-05-06
>
> 我觉得Code Review还是非常有必要的，不光是一些工作时间不长的同事，即使工作10多年的同事，写出的代码都可能会有一些改进之处，code review也是大家交流技术的机会
>
> 目前的公司没有严格的code review流程，这个很难快速形成，只能慢慢来先养成习惯，之后形成文化
>
> 展开

![](media/image44.png)![](media/image45.png)

> ![](media/image46.png)**Jxin**
>
> 2020-05-06
>
> 1.应该。这既是保障项目质量持续优益的手段，也是加速新人融入团队的好方法（达成共同认知，理解团队的协作方式）。
>
> 2.曾经组织过，但流于形式，不了了之。
>
> …
>
> 展开

![](media/image47.png)![](media/image45.png)
