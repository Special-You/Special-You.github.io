---
title: vue+iview导出xls格式的excle
date: 2019-3-05 16:58:04
tags: 
    - vue
    - iview
    
categories: vue iview
description: vue+iview导出xls格式的excle
---


## iview 自带的导出格式为.csv，如果要实现.xls格式的需要引入两个文件Blob.js和Export2Excel.js

### 全局执行以下命令    
```
npm install -S file-saver //用来生成文件的web应用程序
npm install -S xlsx //电子表格格式的解析器
npm install -D script-loader //将js挂在在全局下

```   
### Export2Excel.js里更改
```
require('script-loader!file-saver');
require('script-loader!../../assets/js/Blob'); //主要改这个，路径为到导出的页面位置与Blob.js的位置
require('script-loader!xlsx/dist/xlsx.core.min');

```
### 在main.js里配置  
```
import Blob from './assets/js/Blob.js'
import Export2Excel from './assets/js/Export2Excel'
```  
### 在要做导出操作的页面
```
formatJson(filterVal, jsonData) {
                return jsonData.map(v => filterVal.map(j => v[j]))
            },
exportMeeting() {
                require.ensure([], () => {
                    const {export_json_to_excel} = require('../assets/js/Export2Excel')  //这个地址和页面的位置相关，这个地址是Export2Excel.js相对于页面的相对位置
                    exports(this.queryForm).then(res =>{
                        if(res.data.flag ===1){
                            const tHeader=['会议名称','会议类型','会议开始时间','会议结束时间','市场名字','销量','讲师姓名','参会人数','成交率','老板姓名','老板电话','市场地址','讲师电话'];
                            const filterVal = ['meetingName','typeName','startTime','endTime','marketName','sales','lecturerName','meetingNumber','closeRate','bossName','bossPhone','bossAddress','lecturerPhone']
                            const list = res.data.data;
                            const data = this.formatJson(filterVal, list)
                            export_json_to_excel(tHeader, data, '会议excel')
                        }
                    })
                })
            },

```
```
 <Button type="dashed" icon="ios-cloud-upload-outline" class="add" @click="exportMeeting">导出</Button>
```

### Blob.js和Export2Excel.js下载地址：https://github.com/Special-You/export




