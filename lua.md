# Lua

官网<https://www.lua.org/>下载几百 KB 的 exe 即可在 Windows 上执行 Lua 程序。

大概看了一下 Lua 程序设计第二版,把基础部分过了一遍.对于脚本语言 Lua,印象深刻之处在于它的灵活性、小巧的解析器、可以和 C 语言混编、包含 XML 分析器.若是简单的计算,直接下个未过 M 级别的解析器,也能搞定一些计算和文本处理.鉴于目前用并没有对它有太大需求,暂且告一段落.(有打算把 MATLAB 版的 Kindle 笔记导出改写为 Lua,这样更加方便利用一点.)

1. Lua 用户群体：使用嵌入在某个应用程序中的 Lua 的用户、使用解释器程序的用户、同时使用 Lua 和 C 的用户。
2. `lua -i prog` 执行prog中的程序，然后进入交互模式。
3. 执行程序块的另一种方式，用 dofile 加载程序，然后直接调用：`dofile("lua.lua")  func(var)`

    ```bash
    lua -i prog
    # dofile("lua.lua")
    # x = norm(3.4,1.0)
    # print(x)
    # function norm( x,y )
    #   return (x^2 + y^2)^0.5;
    # end
    ```

4. Lua 程序可用空格和逗号来分句。
5. 标识符组成 字母、数字、下划线，不能以数字开头。
6. 避免以一个下划线开头并跟着多个大写字母，_VAR ，Lua 保留作特殊用途。
7. 有大小写区分。
8. 注释一行 `--`，块注释 `--[[ ]]`，或者一段代码的注释用 `--[[ --]]`。
9. 删除一个变量：`var = nil`。
10. 如果代码以 `#` 开头，那么在加载该文件时解释器将忽略这一行，比如

    ```bash
    #/user/local/bin/lua
    ```

11. 解释器用法

    lua [选项参数] [脚本[参数]]

12. 选项参数 -e 可在命令行输入代码

    ```lua
    lua -e "print(math.sin(12))"
    ```

13. 选项参数 `-l` 用于加载库文件。
14. 在交互式命令中打印用等号 `= math.sin(3)`。
15. 解释器执行前先找一个名叫 `LUA_INIT` 的环境变量，如果找到这个变量，并且其内容为“@文件名”，那么解释器会先执行这个文件。
16. Lua 是动态类型语言，没有类型定义。
17. Lua 的8个基础类型：nil(空)、boolean(布尔)、number(数字)、string(字符串)、userdata(用户自定义类型)、function(函数)、thread(线程)、table(表)。
18. 变量本身“携带类型”，`print(type(10))`。
19. 居然可以这样！`a = print; a("Hello World")`。
20. false 和 nil 为假。
21. number类型表示实数，Lua 没有整型数据。
22. 不能像 C 语言那样修改字符串种的一部分，而需要根据修改创建新的字符串。

    ```lua
    a = "one string"
    b = string.gsub(a, "one", "another")
    print(a)
    print(b)
    ```

23. 一个字符串可以小到包含一本书，也可以大到包含一整本书。
24. 字符串通过单引号或者双引号来界定。
25. 转义序列

    ```text
    \a   响铃   \f   提供表格  \' 单引号
    \b   退格   \n   换行      \" 双引号
    \\ 反斜杠   \v   垂直tab
    ```

26. 可以用数值转义成为字符 `\97` 和 `a` 一样。  
27. 用方括号界定字符串 `str = [[ i am a string ]]`。
28. 在一个字符串和一个数字运算时会将字符串转换为数字 `print("10" + 1)`  但是，这样就不行 `print("Haha" + 1)` 。这种强制转换可能在任何需要的地方都进行，比如 `print(10 .. 20)`。  
29. 字符串连接符号 `..`，连接时前后加空格。  
30. 建议不要使用类似 `"10" + 1` 的强制转换。  
31. 转换成为数字的函数，`tonumber("11")`。  
32. 数字转换成字符 `tostring(10)`。  
33. 取字符串长度用操作符 #，`print(#"hello")`。  
34. table 没有固定的大小，可以动态增加元素到 table。
35. 用 table 可以创建数组、符号表、集合、记录、队列等。
36. 可以用 table 来表示模块（module）、包（package）、对象（object）。
37. 构造一个 table

    ```lua
    a = {}           -- 创建一个 table，并将它的索引存储到 a
    k = "x"
    a[k] = 10        -- key = "x", value = 10
    a[20] = "great"  -- key = 20, value = "great"
    k = 20
    print(a[k])      -- "great"
    a["x"] = a["x"] + 1
    print(a["x"])
    ```

38. 引用同一个 table, `a = {}; b = a;`, 取消引用 `b = nil`。
39. 当没有对 table 的引用时, Lua 的垃圾收集器将删除 table, 并且复用它的内存。  
40. 索引的方法：`a["name"]; a.name`。  
41. 长度操作例子

    ```lua
    print(a[#a])     -- 打印列表 a 中最后一个元素
    a[#a]            -- 删除最后一个值
    a[#a + 1]        -- 将 v 添加到列表末尾
    ```

42. 数组结尾的标志 nil, 如果要取中间含有 nil 的数组, 使用 `table.maxn(a)`。  
43. 函数存储在变量中,可以存储在变量中。  
44. Lua 可以调用 C 编写的函数。  
45. Lua 所有的标准库都是 C 语言编写的。  
46. userdata 可以将任意的 C 语言数据存储到 Lua 变量中。  
47. Lua 支持的操作符有：+(加)、-(减)、*(乘)、/(除)、^(指数)、%(取模)、-(负号)。
48. 关系操作符：`<、>、<=、>=、==、~=`。  
49. 两个不同的索引不相等

    ```lua
    a = {}; a.x = 1;
    b = {}; b.x = 1;
    print(a==b)
    ```

50. 逻辑操作符：and、or、not. `print(5 or 4)`。  
51. 取两数之大：`max = (x > y) and x or y`。  
52. 字符串连接：`print("Hello" .. " World")`。  
53. 操作符优先级：`^`、`not # -`(一元)、`* / %`、`+ -`、`..`、`< > <= >= ~= ==`、`and`、`or`。  
54. table 构造

    ```lua
    days = {"Sunday", "Monday", "Tuesday"}
    a = {x=10, y=20}
    fuse = {x=10, "Sunday"}
    more = {["*"]="mul", [2]="element 2"}
    ```

55. 以0为起始索引, (但下面这样做是不推荐的)

    ```lua
    days = {[0]="Sunday", "Monday", "Tuesday"}
    ```

56. 多重赋值语句：`a,b = 10, 2`, 交换：`x,y = y,x`。  
57. 局部变量仅用于声明它们的那个块：`local x`、`local x=x`。  
58. 尽可能使用局部变量。  
59. 控制语句：`if`、`while`、`repeat`、`for`; `if`、`while`、`for` 以 `end` 结尾, `repeat` 以 `until` 结尾。  
60. if then else

    ```lua
    if a < 0 then a = 0 end
    if a < b then return a else return b end
    -- if .. then .. elseif .. then .. else .. end
    ```

61. while

    ```lua
    a = {"1", "2", "3"}
    local i = 1;
    while a[i] do
      print(a[i]);
      i = i + 1;
    end
    ```

62. repeat, 循环体至少执行一次

    ```lua
    repeat
      line = io.read()
    until line ~= ""
    print(line)
    ```

63. for, 格式

    ```lua
    for var=exp1, exp2, exp3 do
      ...
    end
    ```

    从 exp1 到 exp2, 步长为 exp3, 默认步长为 1

    ```lua
    for i=1,10 do
      print(i)
    end
    ```

    其中 i 是局部变量, 跳出循环用 break。
64. 泛型 for

    ```lua
    for i,v in ipairs(a) do print(v) end
    for k in pairs(t) do print(k) end
    for k,v in pairs(t) do print(v) end
    ```

65. 跳出当前块：break、return, return 可以用于返回值。  
66. 函数的输入参数都需要放入圆括号中,如果参数只有一个 table,那么可以这样写 `f{a=10, y=20}`。  
67. 函数输入参数不足,则初始化为 nil; 参数多余则被丢弃。  
68. 多重返回值

    ```lua
    function disptwo()
      return 2, 3
    end
    -- a, b = disptwo()
    print(disptwo())
    ```

69. 多值返回：`print(unpack({1,2,3}))`,可用于函数变长参数的输入, `f(unpack(var))`。  
70. 对于变长参数包含 nil 的,可用 select

    ```lua
    for i=1,select('#',...) do
    local arg=select(i,...)
    ...
    end
    ```

    `select('#',...)` 返回的变长参数总长包括 nil。  
71. 具名实参

    ```lua
    rename{old="temp.lua", new="temp1.lua"}
    ```

    这样可以方便检查参数,而不必记住它们的位置,比如通过 arg.old、arg.new 来检查参数。

72. 非全局的函数

    ```lua
    Lib = {
      foo = function(x,y) return x + y end,
      goo = function(x,y) return x - y end
    }
    print(Lib.foo(1,1))
    ```

73. 局部函数 `local f = function`。  
74. 尾调用指一个函数在结尾时调用另一个函数, 那么结尾时就无需再返回这个函数, 而直接把结果给输出参数,从而不再暂用栈空间。  

    ```lua
    function f(x) return g(x) end
    -- 下面这个就不符合尾调用
    function f(x) return g(x) + 1 end
    ```

75. Lua 是一种解释性语言。
76. 两个错误处理的例子

    ```lua
    print "enter a number"
    n = io.read("*number")
    if not n then error("invalid input") end
    -- 更加便捷的
    print "enter a number"
    n = assert(io.read("*number"), "invalid input")
    ```

77. assert 的第一个参数为 true 时则返回该参数, 若为 false 则执行第二个语句, 第二个参数不是必须的。
78. dofile 的核心是 loadfile, loadfile 并不处理错误。
79. 从字符串中读取代码

    ```lua
    f = loadstring("i = i + 1")
    i = 5; f();
    print(i)
    ```

80. 加载动态链接库例子

    ```lua
    local path = "/user/local/lib/lua/5.1/socket.so"
    local f = package.loadlib(path, "luaopen_socket")
    ```

81. 数组通过 table 实现,可以根据需求增长。下标可以是任意值,Lua 库以下标为 1 作为起始。

    ```lua
    a = {}
    for i=1, 1000 do
      a[i] = 0
    end
    a = {}
    for i=-5, 5 do
      a[i] = i
    end
    print(a[-2])
    ```

82. 矩阵与多维数组,必须显式创建每一行.可以用这种方式直接创建三角矩阵,比较节省内存。

    ```lua
    mt = {}
    N, M = 3, 4;
    for i=1,N do
      mt[i] = {}      -- 创建新的一行
      for j=1, M do
        mt[i][j] = i+j;
      end
    end

83. 文件读取

    ```lua
    -- 逐行读取并链接
    lcoal buff = ""
    for line in io.lines() do
      buff = buff .. line .. "\n"
    end

    -- 读取整个文件
    io.read("*all")

    -- 用 table 存储,然后用 concat 链接
    -- 暂用内存比第一种方法小
    local t = {}
    for line in io.lines() do
      t[#t + 1] = line
    end
    s = table.concat(t, "\n") .. "\n"
    ```

84. 在 Lua 中,只能设置 table 的元表 (metatable),若要设置其他类型的值的元表,则必须通过 C 代码来完成。通过元表和元方法来实现 table 的操作,比如加法减法。
