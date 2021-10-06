# WinBatteryCheck![](https://img.shields.io/badge/language-bat-green.svg)
一个自动查询、保存并展示电脑损耗情况的批处理工具（windows）

## Table of Contents

- [Background](#background)
- [Contents](#contents)
- [Related Efforts](#related-efforts)
- [Maintainers](#maintainers)
- [Contributing](#contributing)
- [License](#license)



## Background

通过系统命令 powercfg/batteryreport , 用户可以自行查看系统自身的电池报告，其中能看到比较重要的电池容量，日期，电池损耗与使用情况。
本项目对该命令进行了封装，会自动在C盘根目录生成带有时间戳的电池报告，生成完毕会自动打开，非常的直观

## Contents
checkBattery.bat
原理：
```bat
::索取管理员权限
%1 mshta vbscript:CreateObject("Shell.Application").ShellExecute("cmd.exe","/c %~s0 ::","","runas",1)(window.close)&&exit

@echo off & setlocal

::获取时间，并且解决小时小于10时字符串出现空格的问题，并用0占位
set hour=%time:~0,2%

if %hour% lss 10 (set hour=0%hour:~1,2%)

::组装时间戳
set strTime=%Date:~0,4%_%Date:~5,2%_%Date:~8,2%_%hour%_%time:~3,2%_%time:~6,2%

set strPath=C:\battery_report_

::后缀
set strSuffix=.html

::组装文件名
set strFile=%strPath%%strTime%

set strFullFile=%strFile%%strSuffix%

::生成报告
powercfg /batteryreport /output "%strFullFile%"

::打开已生成的报告
cmd /c start %strFullFile%




```
如何使用：
- 下载并双击运行即可

Bug修复：
- 修复了时间戳内带空格导致无法自动打开的bug
- 修复了因为未索取管理员权限导致写入C盘根目录失败的bug


## Related Efforts

## Maintainers

[@DenryDu](https://github.com/DenryDu)

## Contributors

## License

***

Support from you is my greatest encouragement! (您的支持是对我的最大鼓励！)       
