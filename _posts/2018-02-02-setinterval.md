---
title: 前端出现轮训场景如何解决
categories:
  - Frontend
tags:
  - javascript
---

### 场景

在商户填写券报名的时候,需要上传文件xlm给后端审核（上传文件成功后开始请求后端接口，查看服务器解析进度），等审核通过后后端返回一个字段再继续填写信息,这种场景如何处理.

### 步骤解析

1.第一次上传文件ajax请求，


2.上传成功后，后端会返回一个字段{uploadStatus: "success"},然后前端每隔5秒，向后端接口请求,询问解析是否成功。

此时后端会返回解析状态 三个状态
{// 解析完成
    progressStatus: "finished",
    // 其中包括两个状态 文件全部通过或者有个别不通过

}
{// 解析中
    progressStatus: "loading",
}
{// 解析出错
    progressStatus: "error",
    errorMsg: "他妈的系统又挂了",
}
3.只要是 progressStatus 为loading 我们就要继续请求这个接口，否则则显示结果
### 代码实现



代码
```
const query = null;
// 上传文件
function upload （） {
    if (uploadStatus === ’success‘) {
        query = setInterval(()=>{
            ajax().then((res)=>{
                checkout(res.progressStatus);
            });// 请求轮训
        }, 2000);
    }
}

function checkout (progressStatus) {
    if (progressStatus !== 'loading') {
     clearInterval(queryInteral);
   }
}


```



### 个人原创
转载请连接出处