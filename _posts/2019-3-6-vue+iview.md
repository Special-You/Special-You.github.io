---
title: vue+iview导入xls格式的excle
date: 2019-3-05 16:58:04
tags: 
    - vue
    - iview
    
categories: vue iview
description: vue+iview导入xls格式的excle
---




```
<Upload 
                            ref="upload"
                            action="http://"
                            name="file"  //文件字段名
                            :show-upload-list="true"
                            :on-format-error="handleFormatError"
                            :on-success="handleSuccess"
                            :on-error="handleError"
                            :format="['xlsx','xls']">
                        <Button icon="ios-cloud-download-outline" type="dashed">导入</Button>
                    </Upload>

```
```
handleFormatError(file) {
                this.$Notice.warning({
                    title: '文件格式不正确',
                    desc: '文件 ' + file.name + ' 格式不正确，请上传.xls,.xlsx文件。'
                })
            },

 handleSuccess(res, file) {
                if (res.flag === 1) {
                    this.$Message.success("数据导入成功！");
                    this.queryMeetings(1);
                    this.$refs.upload.clearFiles();  //清空文件列表
                } else {
                    this.$Message.error("数据导入失败！")
                }
            },
            handleError(error, file) {
                this.$Message.error("数据导入失败！")
            },
```



