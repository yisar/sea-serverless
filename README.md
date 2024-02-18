# sea-serverless

一种基于 node sea 的可插拔 serverless 机制

## 原理

node sea 本质上是将 `代码逻辑` `inject` 注入到 node.exe 里，进而做到打包单文件

借助这个 inject 机制，我们可以先 inject 一个基座应用，然后再 inject 多个子应用

### before

1. 通过 zip 或打包工具，因为是 node 应用，通过 zip 的方式需要祖传 node_modules 文件，node_modules 压缩解压很慢

2. 通过 ncc 等工具打包 node 模块，可以解决 node_modules 问题，但 ncc 本身打包内置模块就有很多问题

### after

使用 sea 的方式，业务逻辑直接注入到 node.exe 里，不需要 node_modules 也不需要压缩解压，打包工具可以切换到 esbuild（不打包内置模块）

### Run

```
$ npm run copy
$ npm run build:base & npm run build:child
$ npm run inject:base & npm run inject:child
$ ./hello.exe
```


