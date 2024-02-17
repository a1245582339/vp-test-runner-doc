# VP test runner
![Static Badge](https://img.shields.io/badge/vscode-%5E1.83.0-blue) ![Static Badge](https://img.shields.io/badge/License-MIT-blue) ![Static Badge](https://img.shields.io/badge/l10n-zh--cn_en--us-green)

[English](./README.md) | 简体中文

## 一个用于运行Visual Parity测试的工具

## 功能

1. 提供在int环境和线上（支持buildNumber）环境下运行spec文件和单个用例运行VP test的CodeLens。
2. 右键菜单中支持int环境和线上（支持buildNumber）环境下运行VP test。
3. 将spec文件添加为VP test的模板文件，并以其为模板创建新的spec文件。
4. 批量添加flight、localStorage与sessionStorage
### CodeLens

在spec文件中的CodeLens

#### For spec

提供了两种运行测试的方式

![p1](https://cdn.statically.io/gh/a1245582339/picx-images-hosting@master/spec.4mqz1e35buw0.webp)

* ***本地运行*** 是使用本地的代码运行测试.

    相当于执行如下命令

```shell
npm run test:vp -- -- --local --input "suites/xxx"
```

* ***线上运行*** 是使用线上的打包产物运行测试. 

    相当于执行如下命令

```shell
npm run test:vp -- -- --input "suites/xxx"
```


在点击 ***线上运行*** 后, 会出现一个输入框.

![p2](https://cdn.statically.io/gh/a1245582339/picx-images-hosting@master/buildnumber.1t6ig76ulxpc.webp)

你可以将你的buildNumber输入在这里并点击回车，如果保持空白并直接点击回车，则会运行线上版本

#### 单用例运行

这个功能的使用方式和spec文件中的一致。但是由于VP test官方并没有为我们提供运行单个用例的能力，所以我是使用创建临时文件的方式实现的这一功能。所以当你运行了这两个命令后，你的文件夹内会出现一些形如```_temp_xxx.spec.json``` 和 ```_temp_xxx.metadata.json```这样的临时文件

你可以把如下两行加入到你组内的```.gitignore```文件中

```git
_temp_**.spec.json
_temp_**.metadata.json
```
**这两个命令仅用于调试VP test阶段。如果你的单个spec文件中写了非常多的用例，执行单个spec文件会导致运行时间很长，这两个命令可以帮助你减少你的调试时间，但是请不要使用它的baseline**

### 右键菜单

文件夹与*.spec.json文件的右键菜单

![p3](https://cdn.statically.io/gh/a1245582339/picx-images-hosting@master/right-menu-run.3quvsdkcxim0.webp)

这部分功能与在spec文件内执行VP test一致，它额外支持了对文件夹下所有的spec文件执行VP test

### 测试报告通知

由于VP test执行的时间很长，所以我习惯于在运行期间先去做一些其他事情，就导致经常会忘记去查看已经完成了的VP test报告。所以我添加了一个通知栏，来提示我VP test已经结束了。

如果你的VP执行的是单个spec文件或者单个用例，那么你可以在通知栏中直接打开报告。
如果你的VP执行的是一个文件夹，那么你可以在通知栏打开这个文件夹。

![p4](https://cdn.statically.io/gh/a1245582339/image-hosting@master/20231006185258.211w3rinpl1c.webp)

如果你遇到了形如：`File xxx cannot be loaded because running scripts is disabled on this system. For more information, see about_Execution_Policies at https:/go.microsoft.com/fwlink/?LinkID=135170`这样的报错，你需要依照如下步骤去更改PowerShell执行策略。

1. 以管理员身份运行Powershell
2. 执行下面这个命令
```ps1
Set-ExecutionPolicy RemoteSigned
```
3. 输入A并点击回车
![p4](https://cdn.statically.io/gh/a1245582339/image-hosting@master/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20231011161241.7qv7bzoihvc.webp)

4. 重新运行VP test

### VP test 模板
#### 1. 创建一个新模板

使创建新的spec文件更简单，你可以**右键点击spec文件**，并将其添加为模板

你也可以为它起一个自定义的名字。

![add-temp](https://cdn.statically.io/gh/a1245582339/picx-images-hosting@master/addTemp.v5isa757k0w.webp)

![add-temp](https://cdn.statically.io/gh/a1245582339/picx-images-hosting@master/new-file-name.3tcs3pnuwsu0.webp)

#### 2. 使用模板

右键点击文件，并点击**选择一个模板来创建spec文件**

![use template](https://cdn.statically.io/gh/a1245582339/picx-images-hosting@master/create-spec.4lxfjotycrs.webp)

选择一个模板
![select template](https://cdn.statically.io/gh/a1245582339/picx-images-hosting@master/select-temp.5tywgbxa8t80.webp)

输入文件名称并点击回车
![new file name](https://cdn.statically.io/gh/a1245582339/picx-images-hosting@master/temp-name.6h2fhacbg6w0.webp)

#### 3. 删除模板

考虑到删除模板是一个低频操作，我并没有把它添加到右键菜单中。你可以通过点击**F1**然后输入**Delete a VP test template**，然后你可以点选一个模板，它就会被删除。
![delete vp](https://cdn.statically.io/gh/a1245582339/picx-images-hosting@master/del-vp-temp.2d8qus05bkn4.webp)

### 使用右键菜单添加字段
本工具支持了添加三个字段包括: **Flight**, **LocalStorage** 和 **SessionStorage**。但并没有支持删除字段，你可以通过查找/替换来实现删除字段这一功能
![add key](https://cdn.statically.io/gh/a1245582339/picx-images-hosting@master/add-key.f57mre90yzc.webp)
