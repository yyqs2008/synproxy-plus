# synproxy-plus
替换SYNPROXY的SHA1算法


增加了几个函数：
主要是为__cookie_v4_check和__cookie_v4_init_sequence两个函数增加了_hash后缀，除了把SHA1替换成了jhash之外，逻辑上没有变化。
注意：两轮jhash计算我使用了jhash_3words：
1.第一次将daddr作为了inival，这个主要是因为到达本机的attack大部分是针对本机的，daddr的变数小；
2.第二次将daddr省略，且将dport退而求其次作为initval。
以上的考虑是因为在时间序上，只要保证MLS时间窗口内TCP的ISN抗碰撞就好了。
