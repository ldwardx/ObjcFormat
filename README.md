代码格式没有对错之分。但对于团队来讲，阅读他人代码是不可避免的。我们相信，阅读与思考比编码更为重要。而统一的风格无形中会提升阅读体验，提高工作效率。

### 简介

ObjcFormat 是一套格式化 objc 代码的工具，与 git 结合，在本地 commit 时检查代码格式，并提供自动格式化的功能。(非 git 仓库也可使用)

格式整体接近苹果官方风格，参见 [Coding Guidelines for Cocoa](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html)  、[Google Objective-C Style Guide](http://google.github.io/styleguide/objcguide.html) 。

> 注：格式化不会修改实际代码(如变量名、方法名等)。

### 安装

在仓库内执行 **install** 文件。

### 卸载

在仓库内执行 **uninstall** 文件。



------

### 说明

我们有责任 review 提交到远程仓库的每一行改动。对于格式化后的代码也一样。

格式化基于 [clang-format](https://clang.llvm.org/docs/ClangFormat.html) ，一个强大的工具。但不排除一些另类的写法使 clang-format 产生困惑，导致非预期的格式，甚至编译/运行错误。(虽然目前没有遇到，但没有什么比代码的正确性更重要。如果发现此类问题，请及时反馈)

### Review

Commit 时仅会对已暂存的文件进行格式检查，但检查与格式化是应用于整个文件的，而不是本次提交的几行代码。这意味着，我们有责任 review 整个文件的格式化结果。

对于首次格式化，尤其是代码量较大的文件，这并不轻松。但在此之后，每人只需 review 自己提交的部分即可。

虽然只有首次的格式调整最多，但我们不希望 review 成为一种负担。因此，推荐使用代码比对工具(你不会想在这里使用 git diff 的)。

1. #### 工具

   [Beyond Compare](https://www.scootersoftware.com/) 是一款强大的文件比对软件，对于我们这种场景尤其适用。
    

2. #### 安装

   [下载 Beyond Compare](https://www.scootersoftware.com/BCompareOSX-4.2.8.23479.zip) ，打开后选择菜单栏 “Beyond Compare -> 安装命令行工具...” ，安装成功后在终端执行 **git config --global diff.tool bc3** 即可。
    

3. #### 使用

   格式化完成后，在终端执行 **git difftool -y -d --no-symlinks** 即可调起 Beyond Compare，查看所有格式化改动。
    

4. #### 简化

   为了简化操作，我们提供格式化后自动执行上述 difftool 命令的选项。在仓库根目录执行 **call-difftool** 文件即可。

   若要关闭该选项，执行 **cancel-call-difftool** 文件。

### 白名单

加入到白名单中的文件(夹)/代码片段，不会进行格式检查。

- #### 文件(夹)

  在仓库根目录创建 **.format-ignore** 文件，将需要忽略的文件(夹)，以相对于仓库根目录的相对路径，写入该文件，每行一个。

  例如：“Repo/Dir/SubDir/ObjcCode.m” ，若要忽略 ObjcCode.m 文件，需写入 **Dir/SubDir/ObjcCode.m**

  若要忽略 SubDir 文件夹及子文件夹下的所有文件，需写入 **Dir/SubDir/** （注意：需在最后加上 */* ）
   

- #### 代码片段

  在需要忽略的代码片段前后分别加上 **// clang-format** **off** 和 **// clang-format on** 即可。

### 最后

部分工具可以批量格式化文件，但我们不建议在企业项目中使用。批量更改会增加 review 工作量，同时也增大了风险。