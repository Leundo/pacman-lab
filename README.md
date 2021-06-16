# 吃豆人实验
## Introduction
该仓库保存2018级人工智能实验。  

所有改动均只在 `searchAgents.py` 和 `search.py`  

**Version:** `0.1.9`  
进度: 6/8  
Lab 2.6 和 Lab 2.7 未通过评分，有重大缺陷。  

**Version:** `0.1.10`  
进度: 7/8  
Lab 2.6 成功通过😄🍾。  
剩下 Lab 2.7  

**Version:** `0.2.1`  
进度: 8/8 ✅  
全部通过🎇  
接下来可能会完善README。
![Finish](https://s1.ax1x.com/2020/10/11/06qWjA.png)

## Idea
个人的浅薄想法。  

### Lab 2.5
> 在角落迷宫的四个角上面有四个豆。这个搜索问题要求找到一条访问所有四个角落的最短的路径。完成searchAgents.py文件中的CornersProblem搜索问题，你需要重新定义状态，使其能够表示角落是否被访问。

实验报告给出的指令 `python pacman.py -l mediumCorners -p SearchAgent -a fn=bfs,prob=CornersProblem` 要求我们使用 bfs 搜索，prob 类型为 CornersProblem。 我们需要补充 `searchAgent.py` 文件下 `CornersProblem` 类的方法。  
<br>
与问题2类似，我们使用 bfs，区别在于问题2的 state 仅包含坐标信息，而问题5的应该再包含元组 (bool, bool, bool ,bool), 表示是否吃到四个角的豆子。  
**state结构:**  
state: ((x, y), (haveEatenFood1, haveEatenFood2, haveEatenFood3, haveEatenFood4))  
终止状态为 ((_, _), (true, true, ture, ture))  (_代表任意值)

### Lab 2.6
> 构建合适的启发函数，完成searchAgents.py文件中的cornersHeuristic角落搜索问题。  

函数 `cornersHeuristic` 相当于 A\* 算法的 h(x)(这问其实就是用 A\* 改良 L2.5，L2.5 的 h(x) 可以看作是恒等于 0)。  
所以现在只需要在函数 `cornersHeuristic` 里求最短距离的下界就好了。  


### Lab 2.7
> 用尽可能少的步数吃掉所有的豆子。完成searchAgents.py文件中的FoodSearchProblem豆子搜索问题。

这题出现了新的 pron 类型 `FoodSearchProblem`。第一步是先确定 state 的结构。
`print(state)` 得到

    ((2, 3), <game.Grid object at 0x7fb104dd8a50>)
    ((1, 3), <game.Grid object at 0x7fb104dd8ed0>)
    ((3, 3), <game.Grid object at 0x7fb104dd89d0>)
*推荐阅读 game.Grid 类*  
game.Grid 中有方法 `.asList`，`print(state[1].asList())` 得到  

    [(1, 1), (1, 3)]
    [(1, 1)]
    [(1, 1), (1, 3)]
    [(1, 1)]

显然，  
**state结构:**  
state: ((x, y), [食物的坐标列表])  
当[食物的坐标列表]为空时，为终止状态。  

这题我们要完成函数 `foodHeuristic`，作为 A\* 的 h(x)。所以现在只需要在函数 `cornersHeuristic` 里求最短距离的下界就好了。    

### Lab 2.8
> 定义一个优先吃最近的豆子函数是提高搜索速度的一个好的办法。补充完成searchAgents.py文件中的AnyFoodSearchProblem目标测试函数，并完成searchAgents.py文件中的ClosestDotSearchAgent部分，在此Agent当中缺少一个关键的函数：找到最近豆子的函数。  

按题目要求写就好。

