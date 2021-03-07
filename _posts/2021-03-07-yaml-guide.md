---
layout: post
categories: code
---

# YAML :YAML Ain't Markup Language

Yet Another Markup Language

[sample_yaml](sample_yaml_document.md)


## 基本语法规则
- 大小写敏感
- 使用缩进表示层级关系
- 缩进时不允许使用Tab键，只允许使用空格。
- 缩进的空格数目不重要，只要相同层级的元素左侧对齐即可


```yaml

yaml 语法: 
  # YAML使用可打印的Unicode字符，可使用UTF-8或UTF-16。
  # "注解由井字号（ \# ）开始，可以出现在一行中的任何位置
  # 范围只有一行（也就是一般所谓的单行注解）
  list: 
    - 每个清单成员以单行表示
      - "短杠+空白（ \-   ）起始。"
      - ["使用方括号（ [ ] ），" , "逗号+空白（\, ）分开成员" ]

  map:
    - "每个散列表的成员用冒号+空白（ \:   ）分开键值和内容"
    - "或使用大括号（\{\} ）
      并用逗号+空白（ \,   ）分开"
    - "散列表的键值可以用问号 \( \? \)起始
      用来明确的表示多个词汇组成的键值"
  字符:
    - 字符串平常并不使用引号
      "必要的时候可以用双引号 ( \" )或单引号 ( \' )框住"。
    - 使用双引号表示字符串时，
      可用倒斜线（ \ ）开始的转义字符（这跟C语言类似）表示特殊字符。
    - 区块的字符串用缩进和修饰符（非必要）来和其他资料分隔，
      - 换行保留（preserve）（使用符号 | ）
      - 换行折叠（flod）（使用符号 > ）两种方式。
    
  文件:
    - 在单一文件中，可用连续三个连字号（---）区分多个文件。
    - 另外，还有选择性的连续三个点号（ ... ）用来表示文件结尾。

  语句:

    - 重复的内容可使从参考标记星号 ( * )复制到锚点标记（ & ）。
    - 指定格式可以使用两个惊叹号 ( !! )，后面接上名称。
    - 文件中的单一文件可以使用指导指令，使用方法是百分比符号( % )。
      - 有两个指导指令在YAML1.1版中被定义：
      - "%YAML 指导指令，用来识别文件的YAML版本。"
      - " %TAG 指导指令，被用在URI的前缀标记。
       这个方法在标记节点的类型时相当有用。"

  - |
    YAML在使用逗号及冒号时，后面都必须接一个空白字符
  - >
    所以可以在字符串或数值中自由加入分隔符号
    （例如：5,280或http://www.wikipedia.org）
  - |
    另外还有两个特殊符号在YAML中被保留
    有可能在未来的版本被使用--（ @ ）和（ ` ）。

```

## 数据结构

- 对象：键值对的集合，又称为映射（mapping）/ 哈希（hashes） / 字典（dictionary）
- 数组：一组按次序排列的值，又称为序列（sequence） / 列表（list）
- 纯量（scalars）：单个的、不可再分的值

## 对象

`animal: pets`
转为 JavaScript 如下。

`{ animal: 'pets' }`

Yaml 也允许另一种写法，将所有键值对写成一个行内对象。

`hash: { name: Steve, foo: bar } `
转为 JavaScript 如下。

`{ hash: { name: 'Steve', foo: 'bar' } }`

## 数组

```yaml

- Cat
- Dog
- Goldfish
# => [ 'Cat', 'Dog', 'Goldfish' ]

-
 - Cat
 - Dog
 - Goldfish
 #=> [ [ 'Cat', 'Dog', 'Goldfish' ] ]

 animal: [Cat, Dog]
 #=>  animal: [ 'Cat', 'Dog' ] }

```

## 复合结构

<table>
<thead>
<tr>
  <td>yaml</td>
  <td>json object</td>
</tr>
</thead>
<tbody>

<tr>
<td>

```yaml

languages:
 - Ruby
 - Perl
 - Python 
websites:
 YAML: yaml.org 
 Ruby: ruby-lang.org 
 Python: python.org 
 Perl: use.perl.org 

```
</td>
<td>

```js

{ 
  languages: [ 'Ruby', 'Perl', 'Python' ],
  websites: 
   { YAML: 'yaml.org',
     Ruby: 'ruby-lang.org',
     Python: 'python.org',
     Perl: 'use.perl.org' } 
}

```
</td>
</tr>

<tr>
  <td>

  ```yaml

  #数值
  number: 12.30
  #null 用~
  parent: ~ 
  #boolean
  isSet: true
  #时间采用 ISO8601 格式
  iso8601: 2001-12-14t21:59:43.10-05:00
  #日期采用复合 iso8601 格式的年、月、日表示
  date: 1976-07-31

  ```

  </td>
  <td>

  ```js

  // num
  { number: 12.30 }
  // null
  { parent: null }
  //bool
  { isSet: true }
  //time
  { iso8601: new Date('2001-12-14t21:59:43.10-05:00') }
  //date
  { date: new Date('1976-07-31') }

  ```

  </td>
</tr>

<tr>
  <td>

  ```yaml

    #允许使用两个感叹号，强制转换数据类型
    e: !!str 123
    f: !!str true

  ```

  </td>
  <td>

  ```js

  // => json

    { e: '123', f: 'true' }
  

  ```

  </td>
</tr>



  </tbody>
</table>


## string


字符串是最常见，也是最复杂的一种数据类型。

字符串默认不使用引号表示。


<table>
  <thead>
    <tr>
      <td>yaml</td>
      <td>json object</td>
    </tr>
  </thead>
  <tbody>

  <tr>
  <td>

  ```yaml

    #字符串默认不使用引号表示。
    str: 这是一行字符串
    #字符串之中包含空格、特殊字符
    #需放在引号中
    str: '内容： 字符串'
    #单引号和双引号都可以使用
    #双引号不会对特殊字符转义。
    s1: '内容\n字符串'
    s2: "内容\n字符串"

  ```
  
  </td>
  <td>

  ```js

  // str not use ' "
  { str: '这是一行字符串' }
  // str with blank
  { str: '内容: 字符串' }
  // ' => trans  
  // " => not trans
  { s1: '内容\\n字符串', 
    s2: '内容\n字符串' }

  ```
  
  </td>
  </tr>

  <tr>
  <td>

  ```yaml

    #单引号之中如果还有单引号
    #必须连续使用两个单引号转义。

    str: 'labor''s day'

  ```
  
  </td>
  <td>

  ```js

  // ' includes '
  { 
    str: 'labor\'s day' 
  }

  ```
  
  </td>
  </tr>
 
<tr>
  <td>

  ```yaml

  # 字符串可以写成多行
  # 从第二行开始，必须有一个单空格缩进
  str: 这是一段
   多行
   字符串

  ```
  
  </td>
  <td>

  ```js

  // 换行符会被转为空格

  { 
    str: '这是一段 多行 字符串' 
  }

  ```

  </td>
</tr>

<tr><td colspan="2"> 多行文本 </td></tr>

<tr>
  <td>

  ```yaml

  # |+ +表示保留文字块末尾的换行
  # |- -表示删除字符串末尾的换行
  this: |
    Foo
    Bar

    cc
    dd
  s2: |+
   Foo
  s3: |-
   Foo

  ```
  
  </td>
  <td>

  ```js

  // 
  { 
    this: 'Foo\nBar\n',
    that: 'Foo Bar\n' 
  }

  // s3: |-
  //   Foo
  { s1: 'Foo\n', 
    s2: 'Foo\n\n\n', 
    s3: 'Foo' 
  }

  ```
  
  </td>
</tr>

<tr><td colspan="2"> 多行文本 | </td></tr>
<tr>
<td>

  ```yaml

  data: |                                   
   There once was a man from Darjeeling
   Who got on a bus bound for Ealing
       It said on the door
       "Please don't spit on the floor"
   So he carefully spat on the ceiling

  ```

</td>
<td>

  ```js

  /*   
  這裡曾有一個人來自大城市铁岭
  他搭上一班往吉林的公車
    門上這麼說的
    "請勿在地上吐痰"
  所以他小心翼翼的吐在天花板上   
  */

  ```

</td>
</tr>

<tr><td colspan="2"> 多行文本 > </td></tr>
<tr>
<td>

  ```yaml

  data: >
   Wrapped text         # 摺疊的文字
   will be folded       # 將會被收
   into a single        # 進單一一個
   paragraph            # 段落
   
   Blank lines denote   # 空白的行代表
   paragraph breaks     # 段落之間的區隔

  ```

</td>


<td>

  ```js

  /* 

  和 |（保留换行）不同的是，
  >(折叠换行)
  只有空白行才视为换行
  原本的换行字符会被转换成空白字符
  而行首缩进会被去除

  */

  ```

</td>
</tr>


<tr><td colspan="2"> 字符串之中可以插入 HTML 标记 </td></tr>
<tr>
<td>

  ```yaml

message: |
  <p style="color: red">
    段落
  </p>

  ```

</td>


<td>

  ```js

{ 
  message : 
  '\n<p style="color: red">\n  段落\n</p>\n' 
}

  ```

</td>
</tr>


  </tbody>
</table>


## 引用

```yaml

# &用来建立锚点（defaults）
# <<表示合并到当前数据，
# *用来引用锚点

bill-to:  &id001
    street: | 
            123 Tornado Alley
            Suite 16
    city:   East Centerville
    state:  KS

ship-to:  *id001

合并:
  - *id001
  << : *id001
  << : [ *CENTER, *BIG ]


specialDelivery:  >
    Follow the Yellow Brick
    Road to the Emerald City.
    Pay no attention to the
    man behind the curtain.

```


