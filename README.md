# VP test runner
![Static Badge](https://img.shields.io/badge/vscode-%5E1.83.0-blue) ![Static Badge](https://img.shields.io/badge/License-MIT-blue) ![Static Badge](https://img.shields.io/badge/l10n-zh--cn_en--us-green)

English | [简体中文](./README.ZH-CN.md)

## An internal tool of running visualparity test

## Features

1. CodeLens of run VP test of spec and single case with int env and online(support buildNumber) env.
2. Run VP test in right click menu with int env and online(support buildNumber) env.
3. Add spec file to VP test template and create spec file from added template.
4. Batch adding flight, localStorage and sessionStorage.

### CodeLens

CodeLens in spec file

#### For spec

There are 2 types of testing methods.

![p1](https://cdn.statically.io/gh/a1245582339/image-hosting@master/微信图片_20231007083526.6lvbz5uknjo0.webp)

* ***Run Local*** is run the vp test with local server env. 

    Equivalent to executing

```shell
npm run test:vp -- -- --local --input "suites/xxx"
```

* ***Run Online*** is run the vp test with online build. 

    Equivalent to executing

```shell
npm run test:vp -- -- --input "suites/xxx"
```

After click the ***Run Online***, there will show an input.

![p2](https://cdn.statically.io/gh/a1245582339/image-hosting@master/20231006185635.4z2cu5cw9v40.webp)

You can input your buildNumber into this input. If you want to use online build, please leave the input box blank and click the Enter button directly.

#### For test case

The features are same with for spec. But because the vp test dose not provide us the ability to run single test, I added this ability by creating a temporary file. So after you run a single case, some temporary files like ```__temp__xxx.spec.json``` and ```__temp__xxx.metadata.json``` will appear in your folder.

You can remove them before git commit or add this 2 line in ```.gitignore``` file of your group.

```git
_temp_**.spec.json
_temp_**.metadata.json
```

**These two commands are only applicable to the debugging VP test phase. If you have many test cases in a single spec file, which results in a long debugging time for a single case, these two commands can reduce your debugging time, but please do not use its baseline.**

### Right-click menu

Right-click menu of folder and *.spec.json file.

![p3](https://cdn.statically.io/gh/a1245582339/image-hosting@master/20231006133943.mm47r1otadc.webp)

This feature is same with run VP test in spec file. And it supports running all spec files in current folder.

### Report notification

Due to the long running time of VP test, I am accustomed to doing other things during runtime, which often leads to forgetting the VP test report that has ended. So I add a notification to notice me the VP has ended

If the vp test is run by a spec file or a singel case, you can open the report in noticaition.

If the vp test is run by a folder, you can open this folder in noticaition.

![p4](https://cdn.statically.io/gh/a1245582339/image-hosting@master/20231006185258.211w3rinpl1c.webp)

If you get the error seems like: `File xxx cannot be loaded because running scripts is disabled on this system. For more information, see about_Execution_Policies at https:/go.microsoft.com/fwlink/?LinkID=135170`, you need to change the PowerShell Execution Policy by follow steps.

1. Open the Powershell as Administrator

2. Run this Command

```ps1
Set-ExecutionPolicy RemoteSigned
```

3. Select "A" and press Enter
![p4](https://cdn.statically.io/gh/a1245582339/image-hosting@master/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20231011161241.7qv7bzoihvc.webp)

4. Rerun the VP test

### VP test template
1. Create a new template

To make it easier to create a new spec file, you can **right click a exist spec file** and add it to spec template.
![add-temp](https://cdn.statically.io/gh/a1245582339/image-hosting@master/add-temp-left-menu.70d3d5ffib80.webp)
You can customize a name for it that you find convenient.
![add-temp](https://cdn.statically.io/gh/a1245582339/image-hosting@master/input-name.74sep2tcads0.webp)

2. Use template

Right click a folder, and click the **Create a new VP spec file**

![use template](https://cdn.statically.io/gh/a1245582339/image-hosting@master/QQ截图20231117172700.7guxh4xxgbs0.webp)

Select a template
![select template](https://cdn.statically.io/gh/a1245582339/image-hosting@master/select-a-template.in1reuya8nk.webp)

Input a file name and press the Enter
![new file name](https://cdn.statically.io/gh/a1245582339/image-hosting@master/input-new-file-name.6wsaw4dr3mo0.webp)

3. Delete template
Considering that deleting a template is a low-frequency operation, I did not set this feature to the right menu. You can press the **F1** and input the **Delete a VP test template**, you can select a template and it will be deleted.
![delete vp](https://cdn.statically.io/gh/a1245582339/image-hosting@master/delete-vp-temp.5yh9o1uxqb80.webp)

### Add Key by right-click menu
This tool supports 3 fields contains: **Flight**, **LocalStorage** and **SessionStorage**. But it does not support deleting fields, you can delete any fields by **find-and-replace**
![add key](https://cdn.statically.io/gh/a1245582339/picx-images-hosting@master/add-key-en.5o8f7iwzllo0.webp)