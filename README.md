# 用户相关接口
----------
**1.导入用户信息**

  * 访问路径：<https://sdk.yunhetong.com/sdk/userInfo/addUser>
  * 调用方式：POST
  * 接口说明：对接第一步导入用户信息
  * 接口参数：
 
| 字段        | 类型 |说明
|---|---|---|
|appId|String|应用id，19位数字
|appUserId|String|应用在第三方应用那边的id，小于等于49个字
|cellNum|String|电话号码，1开头的11位数字
|userType|Byte|用户类型，1个人2企业4平台
|userName|String|用户名，个人用户名长度小于等于14，企业和平台用户名长度小于等于40
|certifyType|String|实名认证类型，个人用户实名认证类型：1身份证2护照3军官证；企业和平台用户实名认证类型：4营业执照5组织机构代码证6社会那个啥代码
|certifyNumber|String|实名认证号码，身份证，非0开头的15位纯数字或者非0开头的18位纯数字或者非0开头的17位数字加x；护照，长度小于等于20；军官证，长度小于等于20；营业执照，长度小于等于18；组织机构代码证，长度为9；社会那个啥代码，长度小于等于18
|createSignature|String|自动创建签名标志，1为自动创建签名，0为不自动创建签名；
|password|String|应用密码，应用注册时所配置的密码

  
* 接口返回：

|字段|说明
|-|-|
|subCode|操作成功为200，失败返回具体错误code（与异常说明的code相对应），未知错误为520
|message|操作成功返回true，失败返回具体错误（与异常说明的描述相同）
|value|返回获取的值，没有返回值就是空或者null
|code|成功返回200，失败返回520

导入用户信息成功示例：
``` json
{
  "subCode": 200,
  "message": "true",
  "value": {},
  "code": 200
}
```

导入用户信息失败示例：
``` json
{
  "subCode": 10214,
  "message": "实名认证号码已存在",
  "value": null,
  "code": 520
}
```


 * 返回错误码：
 
| subCode   | 描述 |
| --------   | -----  |
|10000|非法的appId!|
|10201|用户名格式错误!|
|10202|用户类型错误!|
|10203|手机号格式错误!|
|10204|实名认证类型错误!|
|10205|实名认证号码格式错误!|
|10206|AppUserId格式错误!|
|10207|用户已存在，信息不一致!|
|10209|该手机号已经存在!|
|10212|用户自动生成签名的参数错误!|
|10214|实名认证号码已存在!|
|10215|该appId下已存在平台用户!|
|10216|企业名已存在!|
|10803|密码不能为空！|
|10804|appId为空或者非法！|
|10805|appId或者密码错误，请重新登录！|


----------
**2.获取用户登录凭证token**

  * 访问路径：<https://sdk.yunhetong.com/sdk/token/getToken>
  * 调用方式：POST
  * 接口说明：获取用户登录凭证，除了导入用户和获取用户登录凭证这个两个接口外，其他所有的接口地址后都要跟token参数
  * 接口参数：
  
| 字段        | 类型 |说明
|---|---|---|
|appId|String|应用id，19位数字
|appUserId|String|应用在第三方应用那边的id，小于等于49个字
|password|String|应用密码，应用注册时所配置的密码
  

* 接口返回： 

|字段|说明
|-|-|
|subCode|操作成功为200，失败返回具体错误code（与异常说明的code相对应），未知错误为520
|message|操作成功返回true，失败返回具体错误（与异常说明的描述相同）
|value|返回获取的值，没有返回值就是空或者null
|code|成功返回200，失败返回520

获取token成功结果示例：
``` json
{
  "subCode": 200,
  "message": "true",
  "value": {
    "token": "TGT-67-g0K2ofZXeoebL4tf33ELAJab0cvAU2aC2DeDJPNnNU3lDHfGvc-cas01.example.org"
  },
  "code": 200
}
```

获取token失败结果示例：
``` json
{
  "subCode": 10004,
  "message": "用户不存在",
  "value": null,
  "code": 520
}
```

 * 返回错误码：
 
| subCode | 说明
|--------| ----- | 
|10004|用户不存在
|10803|密码不能为空！
|10804|appId为空或者非法！
|10805|appId或者密码错误，请重新登录！


----------
**3.修改用户手机号**

  * 访问路径：<https://sdk.yunhetong.com/sdk/userInfo/modifyCellNum?token=xxxxxxxx>
  * 调用方式：POST
  * 接口说明：用户信息变更后，可以调用该接口修改导入到云合同SDK系统中的数据;地址中的token是获取token接口返回的内容
  * 接口参数：
  
| 字段        | 类型 |说明
|---|---|---|
|cellNum|String|电话号码，1开头的11位数字


* 接口返回：  

|字段|说明
|-|-|
|subCode|操作成功为200，失败返回具体错误code（与异常说明的code相对应），未知错误为520
|message|操作成功返回true，失败返回具体错误（与异常说明的描述相同）
|value|返回获取的值，没有返回值就是空或者null
|code|成功返回200，失败返回520

修改用户手机号成功结果示例：
``` json
{
  "subCode": 200,
  "message": "true",
  "value": {},
  "code": 200
}
```

修改用户手机号失败结果示例：
``` json
{
  "subCode": 11003,
  "message": "修改的手机号不能和原手机相同",
  "value": null,
  "code": 520
}
```

 * 返回错误码：
 
| subCode        | 说明 |
| --------   | -----  |
|11001|用户不存在!|
|11003|修改的手机号不能和原手机相同!|
|10209|该手机号已经存在!|
|10801     |登录异常，请重新登录！| 
|10802     |您没有该操作的权限！   |


----------
**4.修改用户名**

  * 访问路径：<https://sdk.yunhetong.com/sdk/userInfo/modifyUserName?token=xxxxxxxx>
  * 调用方式：POST
  * 接口说明：用户信息变更后，可以调用该接口修改导入到云合同SDK系统中的数据;地址中的token是获取token接口返回的内容
  * 接口参数：
  
| 字段        | 类型 |说明
|---|---|---|
|userName|String|用户名，个人用户名长度小于等于14，企业用户名长度小于等于40
|createSignature|String|自动创建签名标志，1为自动创建签名，0为不自动创建签名；
  

* 接口返回：

|字段|说明
|-|-|
|subCode|操作成功为200，失败返回具体错误code（与异常说明的code相对应），未知错误为520
|message|操作成功返回true，失败返回具体错误（与异常说明的描述相同）
|value|返回获取的值，没有返回值就是空或者null
|code|成功返回200，失败返回520

修改用户名成功结果示例：
``` json
{
  "subCode": 200,
  "message": "true",
  "value": {},
  "code": 200
}
```
修改用户名失败结果示例：
``` json
{
  "subCode": 10216,
  "message": "企业名已存在",
  "value": null,
  "code": 520
}
```

 * 返回错误码：
 
| subCode        | 说明 |
| --------   | -----  |
|11001|用户不存在!|
|11002|新信息与老信息不能一致!|
|10201|用户名格式错误!|
|10217|平台用户不能修改用户名!|
|10212|用户自动生成签名的参数错误!|
|10216|企业名已存在!|
|10801     |登录异常，请重新登录！| 
|10802     |您没有该操作的权限！   |


----------
# 合同接口
----------
**1.根据模版生成合同**

 * 访问路径：<https://sdk.yunhetong.com/sdk/contract/templateContract?token=xxxxxxxx>
 * 调用方式：POST
 * 接口说明：根据模版生成合同，功能有：将固定格式字符串替换成指定内容、将固定字符串替换成图片、简单表格操作
 * 接口参数：
 
| 字段        | 类型 |说明
| --------   | -----  | ----- |
| title | String |   合同标题，小于等于40个字     |
| defContractNo        |   String   |   自定义合同编号，方便客户管理合同的一个参数，可以随意传  |
| templateId   |  String    |  合同模板编号，可以在模版列表中查看到  |
| useCer   |  String    |  是否使用存证， 0不使用，1使用；不传或者传空字符串表示不使用存证 |
|param   |  String |  合同占位符参数，json字符串格式，具体说明如下|

param参数示例：

``` java
        {
            "${name1}": "测试",  //普通文本内容占位符；${name1}是模版中设置的占位符名称，“测试”是你要将内容占位符替换成的内容
            "${name2}": "测试",
            "imags": [//图片
                {
                    "${img1}": {//图片占位符名称，${img1}是在模版中设置的
                        "width": 120,  //图片宽度
                        "height": 120, //图片高度
                        "imgType": "png", //图片格式 目前支持格式为：png、jpg、jpeg
                        "content": "......." //图片内容base64编码的字符串
                    }
                },
                {
                    "${img2}": {
                        "width": 120,
                        "height": 120,
                        "imgType": "png",
                        "content": "......."
                    }
                }
            ],
            "tables": [//表格
                {
                    "index": 0,//表示模版中第几个表格,第一个表格为0，第二个表格为1...
                    "table": [//表格内容，按模版中表格列顺序添加
                        {
                            "1": "zhangsan",
                            "2": 10,
                            "3": "杭州市文一西路1118号"
                        },
                        {
                            "1": "lisi",
                            "2": 11,
                            "3": "杭州市文一西路1118号"
                        }
                    ]
                },
                {
                    "index": 2,
                    "table": [
                        {
                            "1": "zhangsan",
                            "2": "杭二中",
                            "3": "杭州市文一西路1118号"
                        },
                        {
                            "1": "lisi",
                            "2": "学军中学",
                            "3": "杭州市文一西路1118号"
                        }
                    ]
                }
            ]
        }
```

* 接口返回：

|字段|说明
|-|-|
|subCode|操作成功为200，失败返回具体错误code（与异常说明的code相对应），未知错误为520
|message|操作成功返回true，失败返回具体错误（与异常说明的描述相同）
|value|返回获取的值，没有返回值就是空或者null
|code|成功返回200，失败返回520

合同生成成功示例：
``` json
{
  "subCode": 200,
  "message": "true",
  "value": {
    "contractId": 1704241653115006
  },
  "code": 200
}
```

合同生成失败示例：
``` json
{
  "subCode": 10715,
  "message": "defContractNo参数非法!",
  "value": null,
  "code": 520
}
```
    
  * 返回错误码：
 
| subCode        | 说明 
| --------   | -----  |
| 10714 |   title参数非法!     |
| 10715 |   defContractNo参数非法!     |
| 10716 |   templateId参数非法!     |
| 10731 |   useCer参数非法!     |
| 10401 |   未找到合同模板!     |
| 10536 |   合同插入表格行失败，对应index表格不存在!     |
| 10537 |   图片占位符替换失败，图片格式错误！     |
| 10538 |   图片占位符替换失败，图片的宽或高未设置！     |
| 10540 |   XX占位符不存在！!     |
|10801     |登录异常，请重新登录！| 
|10802     |您没有该操作的权限！   |
 
----------
**2.上传文件生成合同**

 * 访问路径：<https://sdk.yunhetong.com/sdk/contract/fileContract?token=xxxxxxxx>
 * 调用方式：POST
 * 接口说明：上传文件生成合同
 * 接口参数：
 
| 字段        | 类型 |说明
| --------   | -----  | ----- |
| title | String |   合同标题，小于等于40个字     |
| defContractNo        |   String   |   自定义合同编号，方便客户管理合同的一个参数，可以随便传   |
| useCer   |  int    |  是否使用存证， 0不使用，1使用；不传或者传空字符串表示不使用存证 |
| file   |  File    |  文件内容(字节流) |


* 接口返回：  

|字段|说明
|-|-|
|subCode|操作成功为200，失败返回具体错误code（与异常说明的code相对应），未知错误为520
|message|操作成功返回true，失败返回具体错误（与异常说明的描述相同）
|value|返回获取的值，没有返回值就是空或者null
|code|成功返回200，失败返回520

合同生成成功示例：

``` json
{
  "subCode": 200,
  "message": "true",
  "value": {
    "contractId": 1704241653115006
  },
  "code": 200
}
```

合同生成失败示例：

``` json
{
  "subCode": 10715,
  "message": "defContractNo参数非法!",
  "value": null,
  "code": 520
}
```
    
  * 返回错误码：
  
| subCode        | 说明 
| --------   | -----  |
| 10714 |   title参数非法!     |
| 10715 |   defContractNo参数非法!     |
| 10716 |   templateId参数非法!     |
| 10731 |   useCer参数非法!     |
|10801     |登录异常，请重新登录！| 
|10802     |您没有该操作的权限！   |
 
----------
**3.添加参与者**

  * 访问路径：<https://sdk.yunhetong.com/sdk/contract/addPartner?token=xxxxxxxx>
  * 调用方式：POST
  * 接口说明：合同创建人才能添加参与者且创建人必须是参与者
  * 接口参数：
  
| 字段        | 类型 |说明
| --------   | -----  | ----- |
|contractId     |String | 合同编号
|partners     |String | 参与者列表，josn格式

partners参数示例：
``` java
    [
        {
            "appUserId": "A",       //对接平台用户编号(必填)
            "locationName": "SA"    //模板签名占位符名称，以上传文件生成合同不用传该参数(与keyWord必填其一)
        }, 
        {
            "appUserId": "B",       //对接平台用户编号(必填)
            "locationName": "SB",   //与keyWord同时存在以keyWord为主
            "keyWord": "云合同"     //pdf中签名定位关键字(length<=10)
        }
    ]
```


* 接口返回：  

|字段|说明
|-|-|
|subCode|操作成功为200，失败返回具体错误code（与异常说明的code相对应），未知错误为520
|message|操作成功返回true，失败返回具体错误（与异常说明的描述相同）
|value|返回获取的值，没有返回值就是空或者null
|code|成功返回200，失败返回520

添加参与者成功示例：

``` json
{
  "subCode": 200,
  "message": "true",
  "value": {},
  "code": 200
}
```

添加参与者失败示例：
``` json
{
  "subCode": 10529,
  "message": "合同编号不合法",
  "value": null,
  "code": 520
}
```

 * 返回错误码：
 
| subCode        | 说明 
| --------   | -----  |
|10528     |合同编号不能为空 | 
|10529     |合同编号不合法   |
|10530     |合同参与者不能为空 |
|10531     |合同参与者信息不合法|
|10502     |未找到编号对应合同信息|
|10518     |当前用户不是合同创建者，无法添加参与者|
|10549     |创建者必须是合同参与者|
|10517     |当前合同存在参与者，无法再次添加|
|10534     |合同当前状态无法添加参与者|
|10535     |合同文件尚未生成，请稍后再试|
|10541     |参与者AppUserId不能为空|
|10519     |参与者A、B未导入云平台|
|10542     |参与者A的签名位置不能为空!|
|10521     |参与者A关键字超长!|
|10543     |参与者AKeyWord不存在!|
|10544     |参与者ALocationName不存在|
|10801     |登录异常，请重新登录！| 
|10802     |您没有该操作的权限！   |


----------
**4.合同签署**

针对合同签署，云合同提供了专门的页面，具体请看文档：<https://lvxundev.github.io/yunhetong-sdk-js/>
 
----------
**5.合同自动签署**

 * 访问路径：<https://sdk.yunhetong.com/sdk/contract/signContract?token=xxxxxxxx>
 * 调用方式：POST
 * 接口说明：对接平台方有时需要对某些合同实现自动签署，使用此接口完成自动签署功能，调用者token必须为平台用户
 * 接口参数：
 
| 字段        | 类型 |说明
| --------   | -----  | ----- |
|contractId     |String | 合同编号
|signer     |String| 自动签署者列表 json格式

signer参数示例：

``` java
       [
       "A",     //对接平台用户编号
        "B"      //对接平台用户编号
       ]
```
        
* 接口返回：  

|字段|说明
|-|-|
|subCode|操作成功为200，失败返回具体错误code（与异常说明的code相对应），未知错误为520
|message|操作成功返回true，失败返回具体错误（与异常说明的描述相同）
|value|返回获取的值，没有返回值就是空或者null
|code|成功返回200，失败返回520

合同签署成功示例：

``` json
{
  "subCode": 200,
  "message": "true",
  "value": {},
  "code": 200
}
```

合同签署失败示例：
``` json
{
  "subCode": 10529,
  "message": "合同编号不合法",
  "value": null,
  "code": 520
}
```

  * 返回错误码：
  
| subCode        | 说明 
| --------   | -----  |
|10528     |合同编号不能为空 | 
|10529     |合同编号不合法   |
|10532     |签署者信息不合法 |
|10502     |未找到编号对应合同信息|
|10506     |当前合同无法签署|
|10522     |非平台用户无法多个签署|
|10545     |签署者不能为空|
|10546     |签署者A重复|
|10524     |签署人A不是合同参与者|
|10525     |签署人A已签署合同|
|10801     |登录异常，请重新登录！| 
|10802     |您没有该操作的权限！   |
 
----------
**6.合同作废**

 * 访问路径：<https://sdk.yunhetong.com/sdk/contract/invalid?token=xxxxxxxx>
 * 调用方式：POST
 * 接口说明：合同参与者才能作废
 * 接口参数：
 
| 字段        | 类型 |说明
| --------   | -----  | ----- |
|contractId     |String | 合同编号


* 接口返回：  

|字段|说明
|-|-|
|subCode|操作成功为200，失败返回具体错误code（与异常说明的code相对应），未知错误为520
|message|操作成功返回true，失败返回具体错误（与异常说明的描述相同）
|value|返回获取的值，没有返回值就是空或者null
|code|成功返回200，失败返回520

合同作废成功示例：

``` json
{
  "subCode": 200,
  "message": "true",
  "value": {},
  "code": 200
}
```

合同作废失败示例：

``` json
{
  "subCode": 10529,
  "message": "合同编号不合法",
  "value": null,
  "code": 520
}
```

 * 返回错误码：
 
| subCode        | 说明 
| --------   | -----  |
|10528     |合同编号不能为空 | 
|10529     |合同编号不合法   |
|10502     |未找到编号对应合同信息|
|10503     |当前合同无法作废|
|10504     |该用户无作废权限|
|10547     |未签署的合同不能作废|
|10801     |登录异常，请重新登录！| 
|10802     |您没有该操作的权限！   |


----------
**7.合同列表**

* 访问路径：<https://sdk.yunhetong.com/sdk/contract/list?token=xxxxxxxx>
* 调用方式：GET
* 接口说明：平台用户才能获取合同列表,返回该应用下已完成、已作废的合同
* 接口参数:

| 字段        | 类型 |说明
| --------   | -----  | ----- |
|pageNum     |String | 当前页数，正整数
|pageSize    |String | 每页条数，正整数 （0或空默认返回所有合同）


* 接口返回：  

|字段|说明
|-|-|
|subCode|操作成功为200，失败返回具体错误code（与异常说明的code相对应），未知错误为520
|message|操作成功返回true，失败返回具体错误（与异常说明的描述相同）
|value|返回获取的值，没有返回值就是空或者null
|code|成功返回200，失败返回520

查询合同列表成功示例：

``` json
{
      "subCode": 200, 
      "message": "true", 
      "value": {
        "contractList": [
          {
            "id": 1704011818545002, 
            "title": "dddd", 
            "status": "已作废", 
            "appName": "123321qw", 
            "gmtModify": "2017-04-07 17:04:21", 
            "partnerList": null
          }, 
          {
            "id": 1704061131405000, 
            "title": "dddd", 
            "status": "已完成", 
            "appName": "123321qw", 
            "gmtModify": "2017-04-07 16:41:53", 
            "partnerList": null
          }
        ]
      }, 
      "code": 200
    }
```

查询合同列表失败示例：

``` json
{
  "subCode": 10533,
  "message": "非平台用户无法获取合同列表",
  "value": null,
  "code": 520
}
```

* 返回错误码：

| subCode        | 说明 
| --------   | -----  |
|10533     |非平台用户无法获取合同列表 | 
|10801     |登录异常，请重新登录！| 
|10802     |您没有该操作的权限！   |

----------
**8.合同签署状态详情**

* 访问路径：<https://sdk.yunhetong.com/sdk/contract/detail?token=xxxxxxxx>
* 调用方式：GET
* 接口说明：平台及参与用户均可查看
* 接口参数：

| 字段        | 类型 |说明
| --------   | -----  | ----- |
|contractId     |String | 合同编号


* 接口返回：  

|字段|说明
|-|-|
|subCode|操作成功为200，失败返回具体错误code（与异常说明的code相对应），未知错误为520
|message|操作成功返回true，失败返回具体错误（与异常说明的描述相同）
|value|返回获取的值，没有返回值就是空或者null
|code|成功返回200，失败返回520

查询合同签署状态详情成功示例：

``` json
{
        "subCode": 200, 
        "message": "true", 
        "value": {
        "partnerList": [
        {
            "signStatus": "已签署", 
            "userId": "javaTestUserAAA"
        }, 
        {
            "signStatus": "未签署", 
            "userId": "javaTestUserAAAWE"
        }
        ], 
        "title": "dddd", 
        "status": "已作废"
        }, 
        "code": 200
    }
```

查询合同签署状态详情失败示例：

``` json
{
  "subCode": 10529,
  "message": "合同编号不合法",
  "value": null,
  "code": 520
}
```

* 返回错误码：

| subCode        | 说明 
| --------   | -----  |
|10528     |合同编号不能为空 | 
|10529     |合同编号不合法   |
|10502     |未找到编号对应合同信息|
|10526     |该用户无权限获取合同详情|
|10801     |登录异常，请重新登录！| 
|10802     |您没有该操作的权限！   |


----------
**9.合同下载**

 * 访问路径：<https://sdk.yunhetong.com/sdk/contract/download?token=xxxxxxxx>
 * 调用方式：GET
 * 接口参数：平台及参与用户均可下载
 * 接口参数：
 
| 字段        | 类型 |说明
| --------   | -----  | ----- |
|contractId     |String | 合同编号


 * 返回错误码：
 
| subCode        | 说明 
| --------   | -----  |
|10528     |合同编号不能为空 | 
|10529     |合同编号不合法   |
|10502     |未找到编号对应合同信息|
|10527     |当前合同无法下载|
|10512     |该用户无下载权限|
|10801     |登录异常，请重新登录！| 
|10802     |您没有该操作的权限！   |

* 接口返回： 合同zip流

----------
# 消息相关说明
----------
**1.消息发送**


sdk在合同创建签署等过程中会通过接入方应用注册时填写的接口(https接口)发送消息，以便让接入方平台及时了解合同状态以及进行一些必要的数据记录。

>消息的内容是一串json字符串，对应的参数名为content。消息有三种类型，下面根据消息分类进行各个说明。

>当noticeType为1时，表示该消息是合同普通签署消息。此时返回的参数有content、noticeType、noticeParams(如果对接方有传)、map。
``` java
	{
		"content":"合同\"合同测试合同测试\",用户4441已签署,用户4442已签署!",//消息的文本提示内容
		"noticeType":1,//消息类型
		"noticeParams":"由对接方发送给SDK",//表示对接方传给SDK的自定义消息参数，参数格式由对接方自己定义，建议传json字符串
		"map":{
			"contractId":xxxxxxxxxx,//合同ID
			"contractTitle":"合同名称",//合同标题
			"1243321":0,//“1243321”、“124323”是对接方平台用户id，0表示该用户未签署，1表示该用户已签署
			"124323":1
		}
	}
```

>当noticeType为2时，表示该消息是合同签署完成消息。此时返回的参数有content、noticeType、signDigest、noticeParams(如果对接方有传)、map。
``` java
	{
		"content":"合同\"合同测试合同测试\"已签署完成！",//消息的文本提示内容
		"noticeType":2,//消息类型
		"noticeParams":"由对接方发送给SDK",//表示对接方传给SDK的自定义消息参数，参数格式由对接方自己定义，建议传json字符串
		"map":{
			"contractId":xxxxxxxxxx,//合同ID
			"contractTitle":"合同名称",//合同标题
			"czId":xxxxxxxxxx//存证ID，如果该合同启用存证服务会返回，否则不会返回
		}
	}
```


----------
**2.消息返回**

>接入方平台接收到消息处理完毕后，需要返回处理结果，返回结果也是json字符串。
``` java
	{
		"response":true,//消息处理结果，true表示处理成功，false表示处理失败。
		"msg":"消息处理成功!"//消息处理返回的信息。
	}
```
