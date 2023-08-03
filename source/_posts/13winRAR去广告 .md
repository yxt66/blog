---
title: winRAR去广告
date: 2023-07-21
tag:
- winRAR去广告
categories:
- sofeware
---



{%note success:: winRAR去广告%}





<!-- more -->

## 一、注册并去除弹窗广告（`**亲测有效**`）

​		WinRAR简体中文的个人免费版安装后会有“**评估版本**”的标记，而且每次启动时会有代理商的弹窗广告。

#### 1、访问 WinRAR 中文版官网，选择对应版本，安装时记住安装目录（选择英文或者繁体版，本人亲测简体版无效）

```powershell
官网：https://www.rarlab.com/download.htm
坑：注意是官网地址，而不是国内代理的地址（winrar.com.cn）
```

#### 2、新建一个记事本，将下面的注册码复制到记事本内，保存，并将文件名和后缀修改为 “rarreg.key”。

```shell
RAR registration data
SeVeN
Unlimited Company License
UID=000de082d4cb7aeb1c4f
64122122501c4f740157f1ebdb43aacbe102d6a9507d77b7db6566
54d11f6a4329451f160460fce6cb5ffde62890079861be57638717
7131ced835ed65cc743d9777f2ea71a8e32c7e593cf66794343565
b41bcf56929486b8bcdac33d50ecf7739960a6da6b4e02abc1046a
1de3f23f2ffcb196a8beab698d4c570b1d516ca6da41630a72921f
fb4823a51dc1a276e552c654592b04407bd6d33ceb003b9460394b
adc42308815c9a3831d54b208e11c254d3d71f18a3122935273400
```

#### 3、制作好的 rarreg.key 文件复制到 WinRAR 安装目录，默认安装目录为 C:\Program Files\WinRAR

#### 4、完成。打开 WinRAR，“**评估版本**”标记已消失。

#### 5、参考注册码

```shell
注册码一

RAR registration data
Alexander Aymanov
Single PC usage license
UID=dc1d9fdb26f9be064d83
64122122504d83d04ee243231738b88600fb267f1d3b9632421295
d1048b98780395138be06035c6ab9048e2c5c62f0238f183d28519
aa87488bf38f5b634cf28190bdf438ac593b1857cdb55a7fcb0eb0
c3e4c2736090b3dfa45384e08e9de05c58609e0915bfdc561003a6
755c95e82155892c0f36e7ff4b3d62f55230e8ad51b6756d092d0b
89e5c480d3449cc0c7d9ab1d3d4abb32baf07ebabe0e145e608494
e628198aaef1e665f9d63f719cb57ef19f3443f31a830478060233

注册码二

RAR registration data
yaokai.com
Unlimited Company License
UID=636da5a1e3718a4597b9
641221225097b94b94094a6548ed8365940161a87853d63b09c6ff
0b86c572d75fb683db5960fce6cb5ffde62890079861be57638717
7131ced835ed65cc743d9777f2ea71a8e32c7e593cf66794343565
b41bcf56929486b8bcdac33d50ecf77399608cfb51a0f9e15e798c
57fc8a5e5c3fc69a04ae7d4ec41408c506ff1c90962e165207a4e9
45d426eae53d8849d222b3b26997e5e18b4526596c75d682603e01
1364c589ec5fcea9fa5b796e3fa7437cd080392e5d791757768079

注册码三

RAR registration data
Database Administrators
5 PC usage license
UID=54d582e921e445f1bfe8
6412212250bfe8e73e20bdb947f60ef0da9624150bcf8668412c68
84affda559742bbb686d6071302587655a7ba28d516e17834b7616
47cd79a293eb4c0e4fbf5e9f967e6ed5b28a02418d0ab2549fc4da
19e4644f2345190bf26ff7bcd0c819f12560b57cf28adc164a00c6
3174fcbb69509912e7c7c4793779b941901c6c793b7319cc395ee0
8bddb923fa08fc20019b59d0b246e0ac325d2e5854d4f97a602fc0
a4357b8f857cfb717545410ecad088fb28a2a3cf0dff2102863273

注册码四

RAR registration data
PROMSTROI GROUP
15 PC usage license
UID=42079a849eb3990521f3
641221225021f37c3fecc934136f31d889c3ca46ffcfd8441d3d58
9157709ba0f6ded3a528605030bb9d68eae7df5fedcd1c12e96626
705f33dd41af323a0652075c3cb429f7fc3974f55d1b60e9293e82
ed467e6e4f126e19cccccf98c3b9f98c4660341d700d11a5c1aa52
be9caf70ca9cee8199c54758f64acc9c27d3968d5e69ecb901b91d
538d079f9f1fd1a81d656627d962bf547c38ebbda774df21605c33
eccb9c18530ee0d147058f8b282a9ccfc31322fafcbb4251940582

注册码五

RAR registration data
Carol Thompson
Single PC usage license
UID=b8bc6fb0a8094b9eeb29
6412212250eb294bd5b605e535f7334b6e2e56a9e405a044f60225
c843a161a156aa01684c6035c6ab9048e2c5c62f0238f183d28519
aa87488bf38f5b634cf28190bdf438ac593b1857cdb55a7fcb0eb0
c3e4c2736090b3dfa45384e08e9de05c5860ae8049eaa9443b44f9
faac06b7ced5f95ab06b40a99e850616dc92fc5301fe63c674ea55
3971fefd9e10f300d2a515c74b02f673b7fe5a89fa92f51260a5af
78a306093f5763d6acc779488f5d42e9b044836a837c0424153795
```

## 二、利用工具去除广告（来自网上，本人未使用）

​		此方法在更新 WinRAR 之后会失效，需要再执行一次方可生效。

#### 1、下载免费的编译和反编译工具 Resource Hacker。安装后打开。1、下载免费的编译和反编译工具 Resource Hacker。安装后打开。

```shell
工具官网下载：http://www.angusj.com/resourcehacker/
```

![img](https://raw.githubusercontent.com/yxt66/img/main/img/WinRAR2-1.png)

2、点击 “File” “Open”，找到 WinRAR 的安装目录（默认安装目录为 C:\Program Files\WinRAR），选择 WinRAR.exe，打开。

![img](https://raw.githubusercontent.com/yxt66/img/main/img/WinRAR2-2-202307212306895.png)

#### 3、在左侧栏中依次选择 “String Table” “80 : 2052”，删除 1277 行引号内的内容，用空格代替。

![img](https://raw.githubusercontent.com/yxt66/img/main/img/WinRAR2-3-202307212308327.png)

#### 4、依次点击下图位置的“运行”“保存”按钮，进行编译和保存。

![img](https://raw.githubusercontent.com/yxt66/img/main/img/WinRAR2-4-202307212308111.png)

#### 5、关闭 Resource Hacker，运行 WinRAR，发现弹窗广告彻底消失了！