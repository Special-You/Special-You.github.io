---
title: vue+iview日期转换
date: 2019-3-06 16:58:04
tags: 
    - vue
    - iview
    
categories: vue iview
description: vue+iview日期转换
---


### 问题描述：在Modle里用日期选择器的时候，日期回显，当重新change日期的时候，日期格式才会转变，如果没有点击直接update，此时传入后台的如期格式会有T Z，报错
### 解决办法：定义一个函数转换：
```
changeDate(dateA){
                var dateee = new Date(dateA).toJSON();
                var date = new Date(+new Date(dateee)+8*3600*1000).toISOString().replace(/T/g,' ').replace(/\.[\d]{3}Z/,'');
                return date;
            },
```
然后在提交数据那里
```
 confirm() {
                let params = this.updateMeetingForm;
                params.startTime = this.changeDate(this.updateMeetingForm.startTime);
                params.endTime = this.changeDate(this.updateMeetingForm.endTime);
                console.log(params.startTime,555)
                meetingUpdate(params).then(res => {
                    if (res.data.flag === 1) {
                        this.$Message.success('修改成功！');
                        this.updateMeeting = false;
                        this.queryMeetings(this.current);
                    }
                })
            },

```





