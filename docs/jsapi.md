# BCB钱包DAPP调用原生交互接口文档说明



# 版本&更新记录

| 版本号  | 作者      | 日期       | 更新内容 |
| ------- | --------- | ---------- | -------- |
| v.1.0.0 | bcbwallet | 2019-07-15 | 初始版本 |

---

---



# 功能说明

本文档提供钱包的DAPP访问接口说明。Andriod/IOS通用版本。



# Native

## 1.native.getVersionCode

获取bcb wallet 钱包的版本号

-  调用方式

  ```html
  bcbwallet('native.getVersionCode', null, callback);
  ```

-  callback

  ```html
  function(data) {
  　data.versionCode
  }
  ```

-  代码示例	

  ```
  bcbwallet('native.getVersionCode', null, function (data) {
      alert(JSON.stringify(data));
  });
  ```



## 2.native.getVersionName

 获取 bcb wallet 钱包的版本名称

-  调用方式

  ```html
  bcbwallet('native.getVersionName', null, callback);
  ```

- callback

  ```html
  function(data) {
  　data.versionName
  }
  ```

-  代码示例	

  ```
  bcbwallet('native.getVersionName', null, function (data) {
      alert(JSON.stringify(data));
  });
  ```



## 3.native.openUrl

 通过此方法在 bcb wallet 钱包中打开一个新的 webview页面

-  调用方式

  ```html
  bcbwallet('native.openUrl', params, null);
  ```

-  params

  ```html
  {
  	"url":"https://www.baidu.com", //链接地址
  	"title":"百度", //页面标题
  	"showTitle":true  //true为显示app 导航栏并显示title，false则隐藏app 导航栏
  }
  ```

-  代码示例	

  ```
  bcbwallet('native.openUrl', {
      "url":"https://www.baidu.com",
      "title":"百度",
      "showTitle":true
  }, null);
  ```


## 4.native.goBack

 调用此方法退出当前 webview 界面,回到 app界面

-  调用方式

  ```html
  bcbwallet('native.goBack', null, null);
  ```



## 5.native.scanQRCode

 调用此方法打开 bcb wallet 钱包的相机扫描二维码功能,并把扫码结果返回

-  调用方式

  ```html
  bcbwallet('native.scanQRCode', null, callback);
  ```

-  callback

  ```html
  function(data) {
  　data.scanResult //扫描结果字符串
  }
  ```

-  代码示例	

  ```
  bcbwallet('native.openUrl', null, function (data) {
      alert(JSON.stringify(data));
  });
  ```


## 6.native.screenChange

 调用此方法,可以设置不同的参数强制bcb wallet 钱包进行横竖屏或全屏操作

-  调用方式

  ```html
  bcbwallet('native.screenChange', params, null);
  ```

-  params

  ```html
  {
  	"landType":1, //横竖屏 1：横屏，2：竖屏
  	"fullType":1, //是否全屏显示 1：全屏，2：退出全屏
  }
  ```

-  代码示例	

  ```
  bcbwallet('native.screenChange', {
      "landType":1,
      "fullType":1
  }, null);
  ```


# BCB

## 1.bcb.getWalletsInfo

调用此方法可以获取当前bcb wallet 钱包的所有钱包信息列表(钱包名称和钱包地址)

-  调用方式

  ```html
  bcbwallet('bcb.getWalletsInfo', null, callback);
  ```

- callback

  ```html
  function(data) {
  　data.walletsInfo //所有钱包地址信息
  }
  ****返回钱包列表信息****
  walletsInfo:[
  	{
  		"name":"myWallet",
  		"walletAddr":"bcbPDTi68XwoMgGTwxd7ioZeMHHz7p7ewLtQ"
  	},
  	{
  		"name":"newWallet",
          "walletAddr":"bcbCUh7Zsb7PBgLwHJVok2QaMhbW64HNK4FU"
  	}
  ]
  ```

-  代码示例	

  ```
  bcbwallet('native.getWalletsInfo', null, function (data) {
      alert(JSON.stringify(data));
  });
  ```


## 2.bcb.transfer

 调用此方法可以根据设置的参数进行转账操作,并把转账结果返回

-  调用方式

  ```html
  bcbwallet('bcb.transfer', params, callback);
  ```

-  params

  ```
  {
      "from":"", //转账钱包地址
      "to":"", //转账到的目标地址
      "contractAddr":"", //转账币种的合约地址
      "amount":"", //转账金额
      "note":"" //转账备注
  }
  ```

-  callback

  ```html
  function(data) {
  	data.code, //0为转账成功
    	data.message
  }
  ```

-  代码示例	

  ```
  bcbwallet('native.getWalletsInfo', {
      "from":"bcbCUh7Zsb7PBgLwHJVok2QaMhbW64HNK4FU", //转账钱包地址
      "to":"bcbNg7srN9byDMLGL6tG18WEMFLExpVQqGX5", //转账到的目标地址
      "contractAddr":"bcbLTwDzzZn3Jy8cJGvygWLgpTr9hEdVpWZ9", //转账币种的合约地址
      "amount":"100", //转账金额
      "note":"转账" //转账备注
  }, function (data) {
      alert(JSON.stringify(data));
  });
  ```


## 3.bcb.commonPayUrl

 调用此方法可以打开 bcb wallet 钱包显示当前支付信息,信息校验正确后可以进行支付操作,支付完成后返回支付的状态

-  调用方式

  ```html
  bcbwallet('bcb.commonPayUrl', params, callback);
  ```

-  params

  ```
  {
      "payUrl":"http://172.18.20.156:8080/bcbtest/test2.txt" //支付订单链接
  }
  ```

-  callback

  ```html
  function(data) {
  	data.code, //0为支付成功
    	data.message
  }
  ```

-  代码示例	

  ```
  bcbwallet('bcb.commonPayUrl', {
      "payUrl":"http://172.18.20.156:8080/bcbtest/test2.txt"
  }, function (data) {
      alert(JSON.stringify(data));
  });
  ```



## 4.bcb.commonPayParams

 调用此方法可以打开 bcb wallet 钱包显示当前支付信息,信息校验正确后可以进行支付操作,支付完成后返回支付的状态

-  调用方式

  ```html
  bcbwallet('bcb.commonPayParams', params, callback);
  ```

- params

  ```
  {
    "ver": 2,
    "appUISeg": {
      "referInfo": "使用100BCB购买理财项目",
      "conAddr": "devtest9RcfiWWLH6KpVpbPYYQ55TUncnngSYPES",
      "defaultPayAddr": "devtestLDpP6ggZVgMyq1avLtSvgdYz9NUPmQ2p1",
      "affCode": "devtest7389jV8MMKiaC2Ri9TNXb7z2YDrRddqDR",
      "title": "购买BCB理财项目",
      "value": "100"
    },
    "coinParams": {
      "note": "BCB理财存入",
      "gasLimit": "25000",
      "contractCall": [
        {
          "contractAddr": "devtestLL6sMXu8s2hhFRoZH67Q8fig9djogVi3H",
          "methodParams": [
            {
              "name": "_to",
              "type": "types.Address",
              "value": "devtest4YyjKX5cPA6RkReN3GWcFZ35MVU28PLVy"
            },
            {
              "name": "_value",
              "type": "bn.Number-decimal",
              "value": "100"
            }
          ],
          "methodName": "Transfer",
          "methodRet": ""
        },
        {
          "contractAddr": "devtest9RcfiWWLH6KpVpbPYYQ55TUncnngSYPES",
          "methodParams": [
            {
              "name": "termDays",
              "type": "int64",
              "value": "180"
            }
          ],
          "methodName": "Deposit",
          "methodRet": ""
        }
      ]
    }
  }
  ```

-  callback

  ```html
  function(data) {
  	data.code, //0为支付成功
    	data.message
  }
  ```

- 代码示例	

  ```
  bcbwallet('bcb.commonPayParams', params, function (data) {
      alert(JSON.stringify(data));
  });
  ```



## 5.bcb.signData

 调用此方法利用bcb wallet钱包的底层库进行数据签名,并把签名的数据返回

-  调用方式

  ```html
  bcbwallet('bcb.signData', params, callback);
  ```

-  params

  ```
  {
      "address":"bcbCUh7Zsb7PBgLwHJVok2QaMhbW64HNK4FU", //签名地址
      "signContent":"test" //待签名内容
  }
  ```

-  callback

  ```html
  function(data) {
  	data.address, //签名地址
    	data.signContent, //待签名内容
  	date.pubKey, //公钥
  	data.signedData //签名后内容
  }
  ```

-  代码示例	

  ```
  bcbwallet('bcb.signData', {
      "address":"bcbCUh7Zsb7PBgLwHJVok2QaMhbW64HNK4FU",
      "signContent":"test"
  }, function (data) {
      alert(JSON.stringify(data));
  });
  ```



## 6.bcb.thirdAuth

 调用此方法进行 bcb wallet 钱包的进行授权,并把授权状态返回

-  调用方式

  ```html
  bcbwallet('bcb.thirdAuth', params, callback);
  ```

-  params

  ```
  {
      "nonce":"cpNGXLhwjkVMXrrOvJj1UjwV8v2qftvM", //随机数
      "appID":"10", //业务ID
      "sessionInfo":"RFzLhUreEUM9eCAN0UEJXFXYYyvdctsU" //用户信息
  }
  ```

-  callback

  ```html
  function(data) {
  	data.code, //0为授权成功
    	data.message,
  	data.address //授权登录的钱包地址
  }
  ```

-  代码示例	

  ```
  bcbwallet('bcb.thirdAuth', {
      "nonce":"cpNGXLhwjkVMXrrOvJj1UjwV8v2qftvM",
      "appID":"10",
      "sessionInfo":"RFzLhUreEUM9eCAN0UEJXFXYYyvdctsU"
  }, function (data) {
      alert(JSON.stringify(data));
  });
  ```



# OTC

## 1.otc.openOtc

 调用此方法进入bcb wallet 钱包的OTC模块

-  调用方式

  ```html
  bcbwallet('otc.openOtc', null, null);
  ```



## 2.otc.openFastExchange

 调用此方法进入bcb wallet 钱包的闪兑模块

-  调用方式

  ```html
  bcbwallet('otc.openFastExchange', params, null);
  ```

-  params

  ```
  {
      "inCoin":"DC", //待兑换币种
      "outCoin":"USDX", //目标兑换币种
      "autoFinish":true
  }
  ```

-  代码示例

  ```html
  bcbwallet('otc.openFastExchange', {
      "inCoin":"DC",
      "outCoin":"USDX",
      "autoFinish":true
  }, null);
  ```