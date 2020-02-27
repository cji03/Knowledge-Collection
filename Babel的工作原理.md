### 初识Babel

Babel 是 JavaScript 编译器，主要用于将 ECMAScript 2015+ 版本的代码转换为向后兼容的 JavaScript 语法，以便能够运行在当前和旧版本的浏览器或其他环境中。

Babel的编译过程跟绝大多数其他语言的编译器大致同理，分为三个阶段：

- 解析（parse）：将代码字符串解析成抽象语法树
- 变换（transform）：对抽象语法树进行变换操作
- 生成（generate）：根据变换后的抽象语法树再生成代码字符串

### 解析

1. 词法分析：

将一长段字符串进行’语法单元’级的拆分；

语法单元：语法单元是被解析语法当中具备实际意义的最小单元，通俗点说就是类似于自然语言中的词语。比如说：字符串、数字、运算符、标识符、括号、空格等等。

```JavaScript
if (1 > 0) {
  alert("if \"1 > 0\"");
}
// 可以被拆分成如下数组。
[
 { type: "whitespace", value: "\n" },
 { type: "identifier", value: "if" },
 { type: "whitespace", value: " " },
 { type: "parens", value: "(" },
 { type: "number", value: "1" },
 { type: "whitespace", value: " " },
 { type: "operator", value: ">" },
 { type: "whitespace", value: " " },
 { type: "number", value: "0" },
 { type: "parens", value: ")" },
 { type: "whitespace", value: " " },
 { type: "brace", value: "{" },
 { type: "whitespace", value: "\n " },
 { type: "identifier", value: "alert" },
 { type: "parens", value: "(" },
 { type: "string", value: "\"if 1 > 0\"" },
 { type: "parens", value: ")" },
 { type: "sep", value: ";" },
 { type: "whitespace", value: "\n" },
 { type: "brace", value: "}" },
 { type: "whitespace", value: "\n" },
]
```

2. 语法分析

拆完词后接着进行语义上分析，进行组合；比如说这些个词语之间该如何组合，该如何断句。

有两个概念：

- *语句*：语句是一个具备边界的代码区域，相邻的两个语句之间从语法上来讲互不干扰，调换顺序虽然可能会影响执行结果，但不会产生语法错误
比如return true、var a = 10、if (...) {...}
- *表达式*：最终有个结果的一小段代码，它的特点是可以原样嵌入到另一个表达式
比如myVar、1+1、str.replace('a', 'b')、i < 10 && i > 0等

经过递归/循环等复杂逻辑分析之后可以得到类似如下结果：

```JSON
{
  "type": "Program",
  "body": [
    {
      "type": "IfStatement",
      "test": {
        "type": "BinaryExpression",
        "left": {
          "type": "Literal",
          "value": 1
        },
        "right": {
          "type": "Literal",
          "value": 0
        }
      },
      "consequent": {
        "type": "BlockStatement",
        "body": [
          {
            "type": "ExpressionStatement",
            "expression": {
              "type": "CallExpression",
              "caller": {
                "type": "Identifier",
                "value": "alert"
              },
              "arguments": [
                {
                  "type": "Literal",
                  "value": "if 1 > 0"
                }
              ]
            }
          }
        ]
      },
      "alternative": null
    }
  ]
}
```

就得到了我们常说的AST（抽象语法树）

#### 转换

这一个阶段就是对得到的AST进行加工，通常也是各种plugin介入工作的时候。

#### 生成

将转换完之后的AST，构建成代码字符串。
