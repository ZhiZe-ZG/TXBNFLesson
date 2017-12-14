# 0X04 定义Lua

Lua在官方的Document中给出了其语法的定义.在此我将介绍这些定义,练习EBNF顺便复习Lua.

其实Lua的EBNF定义不太完全,其中的一些名词是通过自然语言描述的.我将尽量把这些内容用形式化的EBNF定义出来.对于不太符合我们刚刚介绍的ISO标准的写法我也会加以改写.

由于Stage介绍EBNF自定义的时候我会采用构造性的顺序,这里我用一种不同的顺序--自顶向下.

## syntax

由于Lua语言以chunk为编译单位.这里我定义Lua的syntax等价于chunk.

```EBNF
syntax = chunk;
```

## chunk和block

```EBNF
chunk = block;
block = {stat}, [retstat];
```

这里我们又用到了两个没有定义过的名词'stat'和'retstat'.它们就是指我们很熟悉的Lua语句和return语句.

## 语句

```EBNF
stat = ';' |
    varlist, '=', explist |
    functioncall |
    label |
    'break' |
    'goto', Name |
    'do', block, 'end' |
    'while', exp, 'do', block, 'end' |
    'repeat', block, 'until', exp |
    'if', exp, 'then', block, {'elseif', exp, 'then', block}, ['else', block], 'end' |
    'for', Name, '=', exp, ',', exp, [',', exp], 'do', block, 'end' |
    
    
    for namelist in explist do block end |
    function funcname funcbody |
    local function Name funcbody |
    local namelist [‘=’ explist]
```

(数一下语句个数)

就是各种语句

体现了嵌套