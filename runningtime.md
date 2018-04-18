# The key thing in complexity theroy - Worst Case Running Time
在计算机科学中，我们研究算法时通常以复杂度和运行时间来衡量算法的好坏。而我们研究复杂度通常在没有说明的情况下研究的是最坏时间复杂度(worst-case complexity/worst-case running time)。

对于这个问题，最理想的结果是我们能为该算法找到一个tight bound(离散数学中的big theta)，这样我们才能够说明我们找的复杂度是精确的。如何来找？如果直接根据big Theta的定义，找到相对应的big omega(lower bound)和big O(upper bound)，如果它们正好相等，那worst case running time的bound必然是tight的。直观上理解就是：我知道这个复杂度最多不能超过某一个表达式，并且最小不能小于某一个表达式，这两个表达式恰好相等，等于把复杂度夹在了中间，那么复杂度必然等于这个表达式。

具体做法：upper bound一般直接分析代码获得，每一步code的最坏情况合在一起得到一个算法的worst case的表达式，这种属于理论上分析。我只知道肯定不能超过这个表达式，但不知道是否能达到这个表达式，这时候我们就需要举具体例子告诉我们其实是可以达到的，这个例子将成为你的lower bound。这个例子一般情况下是具有某种property的一类input，而不是一个特定的input，说白了就是给input限定条件然后缩小了我们研究的范围。比如，我们的input的是一个长度为n的list，当我们在研究worst case lower bound 的时候我们可以限定input为全部为even number的长度为n的list，只要这类input能达到你的要求(和upper bound表达式相等)。通过这个input，总结出lower bound是什么，和upper bound结合(发现正好是同一复杂度，不要惊叹，这不是巧合，原因前面已经说过了)，得出tight bound。
