# My understanding of dynamic programming
dynamic programming, 也就是人们常说的dp，是计算机理论里很关键的一种算法及思想，早饭的时候自己又对这个算法进行了反思，总结如下：


- **dp中最关键的思想是将全局问题分解成子问题(sub-problem),  step-by-step, 找出每一步问题的最优解，最后得出全局问题的最优解。但是divide-and-conquer 一样也是将大问题分解成子问题，根据我的理解，它们的不同之处在于很多divide-and-conquer更强调二分法从而降低时间复杂度，类似于将问题等价平分、组合而得出最终答案。 而dp的所有子问题则可以理解成一条线，在这个线上每一个子问题由小到大从左到右依次被处理，每一个当前的最优解都有可能depend on上一个子问题的最优解**

- **dp与greedy algorithm(贪婪算法)的区别在于greedy在每一步的执行是确定的，确定好了算法，只要按照算法去操作每一步就可以了，不用进行比较进而得出这一步需不需要用到上一步的最优解，而且一般能够确定每一步是子问题的最优解。不同的是，dp的核心就是考虑当前子问题是否采取之前若干步的最优解，也就是说之前每一步的最优解我们都要进行记录，每一步的最优解叫做一个状态(state)，这我会在下面提到**

个人认为dp中最关键的两个要素：1.状态(state) 2.状态转化(state transfer) 其中状态是一种静态的东西，类似于数据，它就一直在那儿，需要的时候我去取；而状态转化则是对状态进行提取和操作，从而更新或得出我们需要的新的状态。就好比著名的面向对象(OO)设计模式(design pattern)中的MVC(Model-View-Controller)中的model和controller，model专门用于存放软件所需要的数据，而controller则专门负责对model中数据的各种操作(operation)。

在dp中状态中存什么信息要直接与我们最后最优解要什么相关、与每一步子问题的最优解相关、与题目所给的关键条件相关。而对于状态转移最关键的是，对于当前步(第n步)，我们是否采用第n个数据，如果采用，结果是第n个和之前若干步中的某一步不产生矛盾的最优解与第n步的组合。如果不采用，则直接照搬n-1步的最优解。这里的关键就是选择与不选择，而标准是，哪个方案更优秀就选择哪个

举个例子，dp中最著名的问题之一，背包问题(KnapSack Problem):

- **状态(state): 在这里，我们发现有几个重要条件， 1.背包能盛放多少价值 2.一共装了几个了 3.背包容量还剩多少，有没有超过限定。 在这里我们发现价值是我们想优化的结果，装了几个是我们想分解的子问题，有没有超过容量是本题的限定条件。所以我们在分解子问题的时候，每一步都要使价值达到子问题的最优，同时记录已经占用多少容量或者还剩多少容量，用遍历(traverse)到第几个来规划子问题。过程中保存所有状态。**

- **状态转移(state transfer): 假设现在我们已知1, 2, ..., k个子问题的最优解和状态，求k+1步子问题的最优解(有点像离散数学中的complete induction/strong induction, 区别在于1～k不一定全用上)。在这里我们要考虑放不放第k+1个。如果第k+1个的重量超过了背包的容量，那就肯定不放；如果没有超过，那就考虑直接照搬k步最优解还是选择第k+1个然后更新之前的选择。在这个过程中，核心就是，在不超过容量的情况下，以最大价值为目标，计算每一步状态然后保存**

由于时间原因，今天只能写这么多，但本文此后可能还会更新，也请大家关注后续