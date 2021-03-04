---
layout: post
title: "python regexp rule"
categories: code
author:
- network
---

![regexp 1](/images/py-regexp-rule/regexp1.png)

```yaml

"[...]"
"{m,n}"
"*"
"+"
"?"
"*?,+?,??"
"{m,n}?"
  # => 只匹配M次
"(...)"
  # group
"(?...)"
  # plus commd
"(?aiLmsux)"
  # aiLmsux 只能在表达式开头
  # aA => 忽略|强制 只ASII
  # iI => 忽略|强制 大小写模式
  # mM => 多行
  # lL => 区域
  # sS => .匹配任何符号
  # xX => 详细表达式


```

![regexp 2](/images/py-regexp-rule/regexp.png)

```yaml

"(?(id/name)yes|no)"
  "(<)?(\w+@w+(?:\w+)+)(?(1)>|$)"
  # => antispam@gmail.com
  # => <antispam@gmail.com>
  # != <antispam@gmail.com
  # != antispam@gmail.com>

"\[Num]"
  demo: "\1 \2... etc."
  desc: 引用子匹配
  "(.+) \1 "
    # => fishC fishC 
    # != fishCfishc
"\A" 
  # => string end 字符串的开始位置
"\Z"
  # => string start 字符串结束位置
"\D"
  # => [^0-9]
"\d"
  # => [0-9]
"\B"
  : "py\B" 
    #=> python py3
    # !=  py py. py!

```

![regexp 3](/images/py-regexp-rule/regexp2.png)

