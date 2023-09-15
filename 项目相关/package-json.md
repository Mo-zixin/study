# name

- 不要使用与核心节点模块相同的名称。
- 不要在名称中输入”js“、”node“。
- 名称可以选择以作用域为前缀，例如 `@myorg/mypackage` 。

## scope 范围

scoped packages 作用域包

所有的npm包都有一个名称。某些包的名称也是有作用域的。

在包名称中使用时，作用域前面有`@`符号后面跟一个斜杠

```
@somescope/somepackagename
```

作用域是一种将相关包组合在一起的方法，并且还会影响有关 npm 处理包的方式的一些事情

### 安装作用域包

作用域内包将安装到常规安装文件夹的子文件夹中，

例如，如果其他包安装在`node_modules/packagename`,

则作用域内模块将安装在 `node_modules/@myorg/packagename`

作用域文件夹 （ `@myorg` ） 只是作用域的名称，前面有一个 `@` 符号，可以包含任意数量的作用域包。

通过按名称引用作用域包来安装它，前面有一个 `@` 符号，在 中 `npm install`

```ts
npm install @myorg/mypackage
```

### 引入作用域包

由于作用域包安装在作用域文件夹中，因此在代码中需要作用域包时，必须包含作用域的名称，例如

```
require('@myorg/mypackage')
```

### 发布作用域包

作用域包可以从 CLI 发布， `npm@2` 也可以发布到支持它们的任何注册表，包括主 npm 注册表。

# version 版本

版本必须可由[node-semver](https://github.com/npm/node-semver)解析，node-semver与npm捆绑在一起作为依赖项。

### [版本规范](https://semver.org/lang/zh-CN/#spec-item-7)

采用 X.Y.Z 的格式，其中 X、Y 和 Z 为非负的整数，且禁止（MUST NOT）在数字前方补零。X 是主版本号、Y 是次版本号、而 Z 为修订号。每个元素必须（MUST）以数值来递增

# description 描述

这是一个字符串。这有助于人们发现您的包

# keywords

将关键字放入其中。它是一个字符串数组。这有助于人们发现您的包，因为它列在 `npm search` 中。

# homepage 主页

项目主页的网址。

```json
"homepage": "https://github.com/owner/project#readme"
```

## bugs 错误

项目问题跟踪器的 URL 和/或应向其报告问题的电子邮件地址。这些对于遇到包问题的人很有帮助。

```json
{
  "url" : "https://github.com/owner/project/issues",
  "email" : "project@hostname.com"
}
```

可以指定一个或两个值。如果只想提供 url，可以将“bugs”的值指定为简单字符串而不是对象。

如果提供了 url，则该 `npm bugs` 命令将使用该 url。

# license 许可证

# 人员字段: author, contributors

“作者”是一个人。“贡献者”是一群人。“person”是具有“名称”字段以及可选的“url”和“email”的对象，如下所示：

````json
{
  "name" : "Barney Rubble",
  "email" : "b@rubble.com",
  "url" : "http://barnyrubble.tumblr.com/"
}
````

# funding 资金

您可以指定一个对象，其中包含一个 URL，该 URL 提供有关帮助资助包开发的方法的最新信息，或者一个字符串 URL，或者指定一个数组

````json
{
  "funding": {
    "type" : "individual",
    "url" : "http://example.com/donate"
  },

  "funding": {
    "type" : "patreon",
    "url" : "https://www.patreon.com/my-account"
  },

  "funding": "http://example.com/donate",

  "funding": [
    {
      "type" : "individual",
      "url" : "http://example.com/donate"
    },
    "http://example.com/donateAlso",
    {
      "type" : "patreon",
      "url" : "https://www.patreon.com/my-account"
    }
  ]
}
````

# files 

可选 `files` 字段是一个文件模式数组，用于描述将包安装为依赖项时要包含的条目

文件模式遵循与 类似的 `.gitignore` 语法，但相反：包括文件、目录或 glob 模式（ `*` 、 `**/*` 等）将使文件在打包时包含在压缩包中。省略该字段将使其默认为 `["*"]` ，这意味着它将包含所有文件

始终包含某些文件:

![image-20230831113017413](C:\Users\youwi\AppData\Roaming\Typora\typora-user-images\image-20230831113017413.png)

# main

主字段是一个模块 ID，它是程序的主入口点。

这应该是相对于包文件夹根目录的模块。

如果未设置，则 `main` 默认为 `index.js` 在包的根文件夹中。

# browser  浏览器

如果您的模块打算在客户端使用，则应使用浏览器字段而不是主字段。这有助于提示用户它可能依赖于 Node.js 模块中不可用的原语

# bin

许多包都有一个或多个可执行文件，它们希望将其安装到 PATH 中。npm 使这变得非常简单（实际上，它使用此功能来安装“npm”可执行文件。）

````json
{
  "bin": {
    "myapp": "./cli.js"
  }
}
````

请确保 中 `bin` 引用的文件以 开头 `#!/usr/bin/env node` ，否则脚本将在没有节点可执行文件的情况下启动！

# man

指定单个文件或文件名数组，以便 `man` 程序查找  指定man文档

```json
{
  "name": "foo",
  "version": "1.2.3",
  "description": "A packaged foo fooer for fooing foos",
  "main": "foo.js",
  "man": "./man/doc.1"
}
```

# directories 目录

## directories.bin 

如果在 中 `directories.bin` 指定目录 `bin` ，则将添加该文件夹中的所有文件

## directories.man

装满手册页的文件夹。糖通过遍历文件夹生成“人”数组。

# repository 存储库

指定代码所在的位置

```json
{
  "repository": {
    "type": "git",
    "url": "https://github.com/npm/cli.git"
  }
}
```

# scripts 

## Pre & Post Scripts 执行脚本前后

```json
{
  "scripts": {
    "precompress": "{{ executes BEFORE the `compress` script }}",
    "compress": "{{ run command to compress files }}",
    "postcompress": "{{ executes AFTER `compress` script }}"
  }
}
```

只需创建另一个具有匹配名称的脚本，并在它们的开头添加“前”或“后”。

## Life Cycle Scripts 生命周期脚本

有一些特殊的生命周期脚本只在某些情况下发生。除了 `pre<event>` 、 `post<event>` 和 `<event>` 脚本之外，还会发生这些脚本。

- `prepare`, `prepublish`, `prepublishOnly`, `prepack`, `postpack`, `dependencies`

### **prepare** 准备

- 运行在包被打包之前，即在`npm publish`和`npm pack`期间
- 在本地`npm install`中运行，不带任何参数
- 在`prepublish`之后运行，但仅在 `prepublishOnly`之前运行 
- 如果通过git安装的包  包含一个prepare脚本，那么它的`dependencies`和`devDependencies`将被安装，并且`prepare`脚本将在包 被打包 和 安装之前运行。
- 若要查看输出，请使用以下命令运行： `--foreground-scripts`

### **prepublish** (DEPRECATED) 预发布（已弃用）

在npm发布期间不运行，但在npm ci和npm安装期间运行。更多信息见下文。

### **prepublishOnly 仅预发布**

在包准备好打包之前运行，仅在npm publish中运行

### **prepack 预包装**

在打包压缩包之前运行（在 “ `npm pack` ”、“” `npm publish` “ 上，以及安装 git 依赖项时）

### **postpack 邮包**

在生成压缩包之后但在移动到其最终目标之前运行（如果有的话，发布不会在本地保存压缩包）

### **dependencies** 

在发生变化时，执行任何修改node_modules目录的操作之后运行

不在全局模式下运行

## [Life Cycle Operation Order 生命周期操作顺序](https://docs.npmjs.com/cli/v9/using-npm/scripts?v=true#life-cycle-operation-order)

# config 

“config”对象可用于设置在升级后保留的包脚本中使用的配置参数。例如，如果包具有以下内容：

````json
{
  "name": "foo",
  "config": {
    "port": "8080"
  }
}
````

# dependencies 依赖

依赖项在将包名称映射到版本范围的简单对象中指定。版本范围是具有一个或多个空格分隔描述符的字符串。依赖项也可以用压缩包或 git URL 来标识。

##  版本范围指定

