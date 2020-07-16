---
date: 2020-07-16 22:22:10
tags:
    - 杂项
---

# ubuntu20.04安装StarUML2

## 存在的问题

- [StarUML官网下载地址](http://staruml.io/download) 提供的最新StarUML3只有AppImage格式的，需要wine才行。所以我选择的是StarUML2。
- StarUML2依赖libgcrypt11和libcurl3。libgcrypt11是ubuntu14.04的依赖库，可以去找deb包解决；而libcurl3不行，由于curl依赖libcurl4，libcurl3和libcurl4冲突，安装libcurl3会导致curl的卸载，从而导致transmission的卸载。



## 解决方案

1、下载StarUML2的deb和libgcrypt11依赖的deb。

[StarUML2官网下载地址](http://staruml-7a0.kxcdn.com/releases-v2/StarUML-v2.8.1-64-bit.deb) 

[libgcrypt11下载地址](http://launchpadlibrarian.net/375021363/libgcrypt11_1.5.3-2ubuntu4.6_amd64.deb) 

libgcrypt11还依赖multiarch-support，[multiarch-support的下载地址](http://launchpadlibrarian.net/416685704/multiarch-support_2.19-0ubuntu6.15_amd64.deb) 

```sh
# cd到下载目录中，然后执行安装命令
sudo apt-get install ./multiarch-support_2.19-0ubuntu6.15_amd64.deb
sudo apt-get install ./libgcrypt11_1.5.3-2ubuntu4.6_amd64.deb
```



2、改变curl的版本，使得它同时支持libcurl3和libcurl4。

```sh
# 这是别人自己重新打包的一个curl版本。
# 原理也很简单，就是让apt-get把libcurl3解释为libcurl4，这样当apt-get要检索starUML依赖的libcurl3时，就会检索到已安装的libcurl4，这样就不会提示找不到依赖了。对于使用没有影响。
sudo add-apt-repository ppa:xapienz/curl34
sudo apt-get update
sudo apt-get install curl
```



3、依赖问题都解决了，就能安装StarUML2了。

```sh
# cd到下载目录中，然后执行安装命令
sudo apt-get install ./StarUML-v2.8.1-64-bit.deb
```



## 破解

```sh
# 修改验证脚本
sudo vi /opt/staruml/www/license/node/LicenseManagerDomain.js
```

破解的原理也比较简单：

对于starUML的验证函数，直接返回一个license信息。这样starUML就会认为你已经有了一个有效的license。

```js
// 在函数validate中添加内容：
function validate(PK, name, product, licenseKey) {
    var pk, decrypted;
	// 破解 - 开始
	return {
		name:"test",
        product:"StartUML",
        licenseType:"vip",
        quantity:"staruml.io",
        licenseKey:"starumllicense"
    };
    // 破解 - 结束
    try {
        pk = new NodeRSA(PK);
        decrypted = pk.decrypt(licenseKey, 'utf8');
    } catch (err) {
        return false;
    }
    var terms = decrypted.trim().split("\n");
    if (terms[0] === name && terms[1] === product) {
        return { 
            name: name, 
            product: product, 
            licenseType: terms[2],
            quantity: terms[3],
            licenseKey: licenseKey
        };
    } else {
        return false;
    }
}
```

