---
title: JS实现Bash现有功能
date: 2022-04-08 15:03:24
tags:
---
> 基于zx这个包，把线上和测试环境的bash脚本，用JS实现下

## reference
https://github.com/google/zx

### shebang
unix - # => sharp, hash or mesh
unix - ! => bang
```
#!interpreter [optional-arg]
#!/usr/bin/env zx
```

#### bash
- https://zhuanlan.zhihu.com/p/353435902?utm_medium=social&utm_oi=1084230223444353024
- vscode编辑器配置


### bash
1. `#!/usr/bin/env bash`：此行是脚本的魔术行，指定运行该脚本的解释器。在这个案例中，它定义了脚本应由Bash( Bourne Again SHell)运行。
   
2. `set -euxo pipefail`：这是bash脚本的一个常见配置，它可以让脚本在出现错误时立即停止，并提供一些有用的调试信息。
   - `set -e`：一旦脚本中的命令返回非零退出状态，脚本就会退出。
   - `set -u`：如果脚本试图使用未设置的变量，脚本会退出。
   - `set -x`：这将在执行每个命令之前打印命令，有助于了解脚本在哪里失败。
   - `set -o pipefail`：如果管道中的任何命令失败，整个管道将失败，即使最后一个命令成功，并返回其成功的状态（0）。

3. `./scripts/download-fonts`：执行"download-fonts"脚本，该脚本可能是用于从特定位置下载一些字体文件。
   
4. `./scripts/prepare-env-vars`：执行"prepare-env-vars"脚本，该脚本可能是用于设置环境变量。

5. `./scripts/setup-sentry-properties`：执行"setup-sentry-properties"脚本，该脚本可能是用于配置Sentry的属性，Sentry是一种用于实时监控和修复错误的应用程序。

6. `./scripts/setup-android-files`：执行"setup-android-files"脚本，可能是用于准备一些Android项目需要的文件或配置。