---
title: npm-link来调试
date: 2020-08-05 16:59:13
tags: 
    - npm 系列
---
> 主体项目拆分出了UI库和核心逻辑js库，在UI库里面调试阶段，除了example，可能还得连具体代码，所以利用npm link进行调试

在被引用的包项目里面运行，执行之后，被引用的包会被链接到全局，路径是 {prefix}/lib/node_modules/<package>
```
npm link
```
在用包的项目里面运行,这样被引用的包会被链接到用包项目的node_modules下面
```
npm link seal_topic_ui
```

之后，只要在被引用包里面有修改，修改会直接生效


#### tips:查看prefix
```
npm config get prefix
```

