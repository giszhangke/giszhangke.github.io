---
title: RHEA接口
date: 2019-09-09 10:46:52
tags: rhea
---



# 人员库(Group)管理相关接口

## 创建人员库

**URL**

```
http://{ip}:{port}/groups
```

**Method**

```
POST
```

**Request**

**字段说明**

| 字段 | 类型   | 是否必填 | 描述                   |
| ---- | ------ | -------- | ---------------------- |
| name | String | 是       | 人员库名称，最多64字节 |

**示例报文**

```
{
    "name":"考勤库"
}
```

**Response**

**报文字段说明**

| 字段    | 类型      | 描述       |
| ------- | --------- | ---------- |
| code    | String    | 状态码     |
| message | String    | 状态描述   |
| data    | **Group** | 人员库信息 |

**Group字段说明**

| 字段    | 类型   | 描述       |
| ------- | ------ | ---------- |
| groupId | Long   | 人员库ID   |
| name    | String | 人员库名称 |

```
{
    "code":"00000000",
    "message":"请求处理成功",
    "data": {
        "groupId":"1",
        "name":"考勤库"
    }
}
```

## 1.2 删除人员库

**URL**

```
http://{ip}:{port}/groups/{groupId}
```

**Method**

```
DELETE
```

**Request**

```
http://127.0.0.1:8080/groups/1
```

**字段说明**

| 字段    | 类型 | 是否必填 | 描述     |
| ------- | ---- | -------- | -------- |
| groupId | Long | 是       | 人员库ID |

**Response**

**报文字段说明**

| 字段    | 类型   | 描述     |
| ------- | ------ | -------- |
| code    | String | 状态码   |
| message | String | 状态描述 |

```
{
    "code":"00000000",
    "message":"请求处理成功"
}
```

## 1.3  修改人员库

**URL**

```
http://{ip}:{port}/groups/{groupId}
```

**Method**

```
PUT
```

**Request**

**字段说明**

| 字段 | 类型   | 是否必填 | 描述       |
| ---- | ------ | -------- | ---------- |
| name | String | 是       | 人员库名称 |

**示例链接**

```
http://127.0.0.1:8080/groups/1
```



**示例报文**

```
{
    "name":"部门考勤库"
}
```

**Response**

**报文字段说明**

| 字段    | 类型      | 描述       |
| ------- | --------- | ---------- |
| code    | String    | 状态码     |
| message | String    | 状态描述   |
| data    | **Group** | 人员库信息 |

**Group字段说明**

| 字段    | 类型   | 描述       |
| ------- | ------ | ---------- |
| groupId | Long   | 人员库ID   |
| name    | String | 人员库名称 |

```
{
    "resCode":"00000000",
    "resMessage":"请求处理成功",
    "data": {
        "groupId":"1",
        "name":"部门考勤库"
    }
}

```

## 1.4 查询人员库

**URL**

```
http://{ip}:{port}/groups/{groupId}?detail={detail}&order={order}&asc={asc}

```

**Method**

```
GET

```

**Request**

**参数说明**

| 字段   | 类型    | 默认值 | 是否必填 | 描述             |
| ------ | ------- | ------ | -------- | ---------------- |
| detail | Boolean | false  | 否       | 是否显示详细信息 |
| order  | String  |        | 否       | 排序属性名       |
| asc    | Boolean | false  | 否       | 是否升序         |

**字段说明**

| 字段    | 类型 | 是否必填 | 描述     |
| ------- | ---- | -------- | -------- |
| groupId | Long | 是       | 人员库ID |

**示例请求**

```
http://127.0.0.1:8080/groups/6957382886236197?detail=true

```

**Response**

**报文字段说明**

| 字段    | 类型      | 描述       |
| ------- | --------- | ---------- |
| code    | String    | 状态码     |
| message | String    | 状态描述   |
| data    | **Group** | 人员库信息 |

**Group字段说明**

| 字段       | 类型             | 描述           |
| ---------- | ---------------- | -------------- |
| groupId    | Long             | 人员库ID       |
| name       | String           | 人员库名称     |
| createTime | Long             | 创建时间       |
| updateTime | Long             | 更新时间       |
| faceCount  | Integer          | 人脸总数       |
| persons    | List<**Person**> | 人员库人员信息 |

**Person字段说明**

| 字段       | 类型 | 描述     |
| ---------- | ---- | -------- |
| id         | Long | 人员ID   |
| groupId    | Long | 人员库ID |
| createTime | Long | 添加时间 |



示例报文

```
{
    "resCode":"00000000",
    "resMessage":"请求处理成功",
    "data": {
        "groupId":"6957382886236197",
        "name":"部门考勤库",
        "createTime": 1566988215177,
        "updateTime": null,
        "faceCount": 5,
        "persons": [
            {
                "id": 7212679378198609,
                "groupId": 6957382886236197,
                "createTime": 1567049082603
            },
            {
                "id": 7212772852457525,
                "groupId": 6957382886236197,
                "createTime": 1567049104889
            }
        ]
    }
}

```

## 1.5 人员库分页查询

**URL**

```
http://{ip}:{port}/groups/list?index={index}&size={size}

```

**Method**

```
GET

```

**Request**

**字段说明**

| 字段  | 类型    | 是否必填 | 默认值 | 描述     |
| ----- | ------- | -------- | ------ | -------- |
| index | Integer | 否       | 1      | 页面索引 |
| size  | Integer | 否       | 10     | 单页大小 |

**示例请求**

```
http://127.0.0.1:8080/groups/list?index=1&size=10

```

**Response**

**报文字段说明**

| 字段    | 类型     | 描述           |
| ------- | -------- | -------------- |
| code    | String   | 状态码         |
| message | String   | 状态描述       |
| data    | **Page** | 当前页数据信息 |

**Page字段说明**

| 字段    | 类型            | 描述               |
| ------- | --------------- | ------------------ |
| records | List<**Group**> | 当前页的人员库信息 |
| total   | Long            | 总记录数           |
| size    | Long            | 单页大小           |
| current | Long            | 当前页索引         |
| pages   | Long            | 总页数             |

**Group字段说明**

| 字段    | 类型   | 描述       |
| ------- | ------ | ---------- |
| groupId | Long   | 人员库ID   |
| name    | String | 人员库名称 |

示例报文

```
{
  "code": "00000000",
  "message": "请求处理成功",
  "data": {
    "records": [
      {
        "name": "考勤库3",
        "groupId": 2545471344193566
      },
      {
        "name": "考勤库5",
        "groupId": 2874659192295505
      },
      {
        "name": "考勤库5",
        "groupId": 2874792139149365
      },
      {
        "name": "考勤库5",
        "groupId": 2876092402688004
      },
      {
        "name": "考勤库5",
        "groupId": 2879365360681030
      },
      {
        "name": "考勤库5",
        "groupId": 2881833100435499
      },
      {
        "name": "考勤库5",
        "groupId": 2884859131363397
      },
      {
        "name": "考勤库5",
        "groupId": 2885922563604485
      },
      {
        "name": "考勤库",
        "groupId": 2917096048607258
      },
      {
        "name": "考勤库",
        "groupId": 3666008493572184
      }
    ],
    "total": 115,
    "size": 10,
    "current": 1,
    "orders": [],
    "searchCount": true,
    "pages": 12
  }
}

```



# 2. 人员（person）管理相关接口

## 2.1 人员创建

- 接口地址：[http://{ip}:{port}/persons]()
- 请求方式：POST
- 请求参数：

| 参数名   | 参数类型 | 备注                                            |
| -------- | -------- | ----------------------------------------------- |
| groupId  | String   | 人脸库id                                        |
| img      | String   | 图片地址（可选）                                |
| imgType  | Integer  | 图片类型（1:url,2:base64,3:fullpath,4:feature） |
| name     | String   | 名字（可选）                                    |
| cardId   | String   | 证件号码（可选）                                |
| phoneNum | String   | 手机号码（可选）                                |

- 返回参数：

| 参数名   | 参数类型 | 备注                     |
| -------- | -------- | ------------------------ |
| personId | Long     | 人员Id                   |
| groupId  | Long     | 人员库Id                 |
| faceId   | Long     | 人脸id（有人脸则返回）   |
| imageId  | Long     | 图片Id（有图片则返回）   |
| imageUrl | String   | 图片路径（有图片则返回） |

- 请求参数示例

```json
{
	"groupId": 1,
	"img": "https://pic2.zhimg.com/80/4a9fe6359190f68621f650a71bf6c2e9_hd.jpg",
	"imgType": 1
}

```

- 返回参数示例

```json
{
    "code": "00000000",
    "message": "请求处理成功",
    "data": {
        "personId": 10175593676533766,
        "groupId": 1,
        "imageId": 10175593466818599,
        "faceId": 10175593861083218,
        "imageUrl": "/Users/neal/Neal/rhea-temp/1567755496367.jpg"
    }
}

```

## 2.2 给人员添加图片

- 接口地址：[http://{ip}:{port}/persons/addFace]()
- 请求方式：POST
- 请求参数：

| 参数名   | 参数类型 | 备注                                              |
| -------- | -------- | ------------------------------------------------- |
| personId | Long     | 人员Id                                            |
| img      | String   | 图片（可以是url，base64图片，推荐使用base64图片） |
| imgType  | Integer  | 图片类型（1:url,2:base64,3:fullpath,4:feature）   |

- 返回参数：

| 参数名   | 参数类型 | 备注   |
| -------- | -------- | ------ |
| personId | Long     | 人员id |
| faceId   | Long     | 人脸id |
| imageId  | Long     | 图片id |

- 请求参数示例

```json
{
    "personId": 5082451604344903,
    "img": "https://pic2.zhimg.com/80/4a9fe6359190f68621f650a71bf6c2e9_hd.jpg",
    "imgType": 1
}

```

- 返回参数示例

```json
{
    "code": "00000000",
    "message": "请求处理成功",
    "data": {
        "personId": 5082451604344903,
        "groupId": 1,
        "imageId": 10175520062304344,
        "faceId": 10175520955691034,
        "imageUrl": "/Users/neal/Neal/rhea-temp/1567755471644.jpg"
    }
}

```

## 2.3 删除人员

- 功能：
  删除 person，删除person 对应的face，删除face对应 facego 中的face
- 接口地址：[http://{ip}:{port}/persons/{{personId}}]()
- 请求方式：DELETE
- 请求参数：

| 参数名   | 参数类型 | 备注   |
| -------- | -------- | ------ |
| personId | Long     | 人员id |

- 返回参数：

|参数名|参数类型|备注|
|---|---|---|

- 请求参数示例

```json

```

- 返回参数示例

```json
{
    "code": "00000000",
    "message": "请求处理成功"
}

```

## 2.4 删除人员中的人脸图片

- 功能：
  找到 person，删除person 对应的face，删除face对应 facego 中的face
- 接口地址：[http://{ip}:{port}/persons/removeFace]()
- 请求方式：POST
- 请求参数：

| 参数名   | 参数类型 | 备注   |
| -------- | -------- | ------ |
| personid | Long     | 人员id |
| faceId   | Long     | 人脸Id |

- 返回参数：

|参数名|参数类型|备注|
|---|---|---|

- 请求参数示例

```
{
    "faceId": 4442842209873926,
    "personId": 4442842079850527
}

```

- 返回参数示例

```json
{
    "code": "00000000",
    "message": "请求处理成功"
}

```

## 2.5 人员创建（上传图片）

- 接口地址：[http://{ip}:{port}/persons/form]()
- 请求方式：POST
- 请求参数：

| 参数名  | 参数类型 | 备注     |
| ------- | -------- | -------- |
| groupId | String   | 人脸库id |
| file    | file     | 图片文件 |

- 返回参数：

| 参数名   | 参数类型 | 备注   |
| -------- | -------- | ------ |
| personId | Long     | 人员Id |
| faceId   | Long     | 人脸id |
| imageId  | Long     | 图片Id |

- 请求参数示例

```json
{
	"groupId": 1,
	"file": "待上传文件"
}

```

- 返回参数示例

```json
{
    "code": "00000000",
    "message": "请求处理成功",
    "data": {
        "faceId": 5505549287763996,
        "personId": 5505549027717203,
        "imageId": 5505547933003873
    }
}

```

# 3. 人脸（Face）管理相关接口

## 3.1 人脸特征提取 

- 接口地址：[http://{ip}:{port}/faces/feature]()
- 请求方式：POST
- 请求参数：

| 参数名 | 参数类型 | 备注       |
| ------ | -------- | ---------- |
| img    | String   | 待识别图片 |

- 返回参数：

| 参数名           | 参数类型 | 备注                                   |
| ---------------- | -------- | -------------------------------------- |
| imageId          | string   | 图片id                                 |
| feature          | string   | 人脸特征                               |
| faceTotalScore   | float    | 人脸质量总分                           |
| lightScore       | float    | 光照分                                 |
| maskScore        | float    | 口罩分                                 |
| clarityScore     | float    | 清晰度分                               |
| glassesScore     | float    | 是否戴眼镜分数                         |
| mouthScore       | float    | 闭嘴分数                               |
| faceClarityScore | float    | 人脸清晰度分数                         |
| sunGlassesScore  | float    | 带墨镜🕶分数                            |
| age              | integer  | 年龄                                   |
| gender           | integer  | 性别 1男 2女 0未知                     |
| nation           | integer  | 国籍 1中国人 2外国人                   |
| ageGroup         | integer  | 年龄段 1小孩 2中年人 3老人             |
| faceDirect       | string   | 正脸 侧脸                              |
| race             | integer  | 人种 1黄种人 2黑种人 4白种人 8新疆人   |
| pitch            | float    | 人脸旋转角 pitch                       |
| yaw              | float    | 人脸旋转角 yaw                         |
| roll             | float    | 人脸旋转角 roll                        |
| x                | float    | 人脸框 x                               |
| y                | float    | 人脸框 y                               |
| width            | float    | 人脸框 width                           |
| height           | float    | 人脸框 height                          |
| printFaceScore   | float    | 是否黑白打印纸张，越大表示越可能是真人 |

- 请求参数示例

```json
{
	"img": "https://c-ssl.duitang.com/uploads/item/201502/06/20150206230530_cXFr5.thumb.700_0.jpeg"
}

```

- 请求成功返回示例

```json
{
    "code": "00000000",
    "message": "请求处理成功",
    "data": {
        "feature": "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",
        "faceTotalScore": 0.7029,
        "lightScore": 0.8000,
        "maskScore": 0.9999,
        "clarityScore": 0.8623,
        "glassesScore": 0.0000,
        "mouthScore": 0.1587,
        "faceClarityScore": 0.9112,
        "sunGlassesScore": 0.0000,
        "age": 25,
        "gender": 2,
        "nation": 0,
        "ageGroup": 0,
        "faceDirect": "0.9531",
        "race": 1,
        "pitch": -7.1051,
        "yaw": -7.1140,
        "roll": -8.4284,
        "x": 201.0000,
        "y": 245.0000,
        "width": 259.0000,
        "height": 259.0000,
        "printFaceScore": 0.9996
    }
}

```

## 3.2 人脸1:1，人脸比对

- 接口地址：[http://{ip}:{port}/faces/verification]()
- 请求方式：POST
- 请求参数：

| 参数名 | 参数类型 | 备注     |
| ------ | -------- | -------- |
| faceA  | String   | 图片1 Id |
| faceB  | String   | 图片2 Id |

- 返回参数：

| 参数名 | 参数类型 | 备注       |
| ------ | -------- | ---------- |
| score  | float    | 相似度分值 |

- 请求参数示例 

```json
{
    "faceA": "3592582751305823",
    "faceB": "3592582751305823"
}

```

- 请求成功返回示例

```json
{
    "code": "00000000",
    "message": "请求处理成功",
    "data": {
        "score": 0.9993
    }
}

```

## 3.2.1 人脸比对 1：1 （上传图片）

- 接口地址：[http://{ip}:{port}/faces/1vs1]()
- 请求方式：POST
- 请求参数：

| 参数名    | 参数类型 | 备注      |
| --------- | -------- | --------- |
| faceAPath | String   | 图片1地址 |
| faceBPath | String   | 图片2地址 |

- 返回参数：

| 参数名 | 参数类型 | 备注       |
| ------ | -------- | ---------- |
| score  | float    | 相似度分值 |

- 请求参数示例 

```json
{
    "faceAPath": "https://pic1.zhimg.com/80/949b9ca035184990d7d34b2fc12ef770_hd.jpg",
    "faceBPath": "https://pic1.zhimg.com/80/949b9ca035184990d7d34b2fc12ef770_hd.jpg"
}

```

- 请求成功返回示例

```json
{
    "code": "00000000",
    "message": "请求处理成功",
    "data": {
        "score": 0.9993
    }
}

```

## 3.3 人脸检测

- 接口地址：[http://{ip}:{port}/faces/detection]()
- 请求方式：POST
- 请求参数：

| 参数名 | 参数类型 | 备注       |
| ------ | -------- | ---------- |
| img    | String   | 待识别图片 |

- 返回参数：

| 参数名 | 参数类型 | 备注           |
| ------ | -------- | -------------- |
| faces  | Array    | 图片中人脸信息 |

- 请求参数示例

```json
{
	"img": "https://blog.aipanpan.com/wp-content/uploads/2018/01/97b46efa6d03c7a74bde83ace3eb3805.jpg"
}

```

- 返回参数示例

```json
{
    "code": "00000000",
    "message": "请求处理成功",
    "data": [
        {
            "x": 309.0,
            "y": 170.0,
            "width": 73.0,
            "height": 73.0
        },
        {
            "x": 206.0,
            "y": 148.0,
            "width": 82.0,
            "height": 82.0
        }
    ]
}

```

## 3.4 人脸1:N识别 单、多库检索

- 接口地址：[http://{ip}:{port}/faces/identification]()
- 请求方式：POST
- 请求参数：

| 参数名       | 参数类型 | 备注                           |
| ------------ | -------- | ------------------------------ |
| faceId       | String   | 人脸id                         |
| groupIds     | Array    | 人脸库id集合                   |
| topN         | Integer  | topN大小，最大10000            |
| thresholdMin | float    | 阈值下限（阈值范围0.0-1.0)可选 |
| thresholdMax | float    | 阈值上限（阈值范围0.0-1.0)可选 |

- 返回参数：

| 参数名    | 参数类型 | 备注         |
| --------- | -------- | ------------ |
| faceId    | Long     | 人脸id       |
| groupIds  | Array    | 人脸库id集合 |
| faceCount | Long     | 人脸数量     |
| faces     | Array    | 人脸集合     |
| faceId    | Long     | 人脸id       |
| score     | Float    | 相似度分值   |

- 请求参数示例

```json
{
    "faceId": 10175520955691034,
    "groupIds": [1,6957382886236197,2],
    "topN": 10,
    "thresholdMin": 0.5,
    "thresholdMax": 0.8
}

```

- 请求成功返回参数示例

```json
{
    "code": "00000000",
    "message": "请求处理成功",
    "data": {
        "faceId": 7996807728046159,
        "groupIds": [
            1,
            6957382886236197,
            2
        ],
        "facesCount": 10,
        "faces": [
            {
                "faceId": 7299112453505065,
                "score": 0.7370124
            },
            {
                "faceId": 7305379372798001,
                "score": 0.7370124
            },
            {
                "faceId": 7305367716827192,
                "score": 0.7370124
            },
            {
                "faceId": 7305358501941336,
                "score": 0.7370124
            },
            {
                "faceId": 7305349618405432,
                "score": 0.7370124
            },
            {
                "faceId": 7305340168638492,
                "score": 0.7370124
            },
            {
                "faceId": 7305321449459760,
                "score": 0.7370124
            },
            {
                "faceId": 7302999654715440,
                "score": 0.7370124
            },
            {
                "faceId": 7302933372129356,
                "score": 0.7370124
            },
            {
                "faceId": 7302824454443027,
                "score": 0.7370124
            }
        ]
    }
}

```

## 3.5 人脸添加

- 接口地址：[http://{ip}:{port}/faces]()
- 请求方式：POST
- 请求参数：

| 参数名  | 参数类型 | 备注     |
| ------- | -------- | -------- |
| groupId | Long     | 人脸库id |
| img     | String   | 图片地址 |

- 返回参数：

| 参数名           | 参数类型 | 备注                                   |
| ---------------- | -------- | -------------------------------------- |
| id               | String   | 人脸id                                 |
| groupId          | String   | 人脸库id                               |
| facePath         | string   | 图片地址                               |
| feature          | String   | 人脸特征                               |
| faceTotalScore   | float    | 人脸质量总分                           |
| lightScore       | float    | 光照分                                 |
| maskScore        | float    | 口罩分                                 |
| clarityScore     | float    | 清晰度分                               |
| glassesScore     | float    | 是否戴眼镜分数                         |
| mouthScore       | float    | 闭嘴分数                               |
| faceClarityScore | float    | 人脸清晰度分数                         |
| sunGlassesScore  | float    | 带墨镜🕶分数                            |
| age              | integer  | 年龄                                   |
| gender           | integer  | 性别 1男 2女 0未知                     |
| faceDirect       | string   | 正脸 侧脸                              |
| race             | integer  | 人种 1黄种人 2黑种人 4白种人 8新疆人   |
| pitch            | float    | 人脸旋转角 pitch                       |
| yaw              | float    | 人脸旋转角 yaw                         |
| roll             | float    | 人脸旋转角 roll                        |
| x                | float    | 人脸框 x                               |
| y                | float    | 人脸框 y                               |
| width            | float    | 人脸框 width                           |
| height           | float    | 人脸框 height                          |
| printFaceScore   | float    | 是否黑白打印纸张，越大表示越可能是真人 |
| createTime       | long     | 创建时间                               |
| updateTime       | long     | 更新时间                               |

- 请求参数示例

```json
{
    "groupId": 1,
    "img": "https://pic2.zhimg.com/80/4a9fe6359190f68621f650a71bf6c2e9_hd.jpg"
}

```

- 请求成功返回参数示例

```json
{
    "code": "00000000",
    "message": "请求处理成功",
    "data": {
        "id": 5027406693167196,
        "groupId": 1,
        "gender": 2,
        "facePath": "https://pic2.zhimg.com/80/4a9fe6359190f68621f650a71bf6c2e9_hd.jpg",
        "feature": "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",
        "faceTotalScore": 0.7337,
        "lightScore": 0.7255,
        "maskScore": 0.9986,
        "clarityScore": 0.8214,
        "glassesScore": 0.0000,
        "mouthScore": 0.0274,
        "faceClarityScore": 0.8732,
        "sunGlassesScore": 0.0000,
        "faceDirect": "0.9238",
        "race": 1,
        "pitch": -9.2046,
        "yaw": -11.8563,
        "roll": 3.1360,
        "x": 164.0000,
        "y": 74.0000,
        "width": 112.0000,
        "height": 112.0000,
        "printFaceScore": 0.0235,
        "age": 26,
        "createTime": 1566528072996,
        "updateTime": 1566528072996
    }
}

```

## 3.6 人脸删除

- 接口地址：[http://{ip}:{port}/faces/{{faceId}}]()
- 请求方式：DELETE
- 请求参数：

| 参数名 | 参数类型 | 备注   |
| ------ | -------- | ------ |
| faceId | Long     | 人脸id |

- 返回参数：

| 参数名 | 参数类型 | 备注 |
| ------ | -------- | ---- |
|        |          |      |



- 请求参数示例

```json

```

- 请求成功返回参数示例

```json
{
    "code": "00000000",
    "message": "请求处理成功"
}

```

# 附录

## 错误码表

待补充