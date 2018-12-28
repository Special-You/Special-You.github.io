---
title: vue
date: 2018-12-15 16:19:04
tags: vue
categories: vue
description: 封装接口请求
---

## 封装promise
```
import axios from 'axios';

export function fetch(options) {
  return new Promise((resolve, reject)=>{
      var _token = localStorage.getItem('d_token');
    const instance = axios.create({
      //instance 创建一个axios实例，可以自定义配置，可在axios文档中查看详情
      //所有的请求都会带上这些配置，比如全局都要用的身份信息等。
      headers: {
        'Content-Type':'application/json',
        'token':_token
      },
      timeout:3000//超时
    });

    //请求拦截器
    instance.interceptors.request.use(config=>{
      //在发送请求前
      if(config.method==='POST'){
        config.data = JSON.stringify(config.data);
      }
      return config;
    },err=>{
      //对请求错误做些什么
      return Promise.reject(err);
    });

    //响应拦截器
    instance.interceptors.response.use(res=>{
      //在响应前
      return res;
    },err=>{
      //对响应错误做些什么
      return Promise.reject(err);
    });

    instance(options)
      .then(res=>{ //then请求成功之后进行的操作
      resolve(res);//把请求到的数据发送引用请求的地方
    })
      .catch(err=>{
        reject(err);
      })
  });
}

```


## 定义全局的接口地址
```
export default {
  //serverUrl:'http://47.105.115.54',
  serverUrl:'http://192.168.1.17:8080',
  //接口代理配置
}
```

## 所有的接口函数
```
import {fetch} from "./fetch";
import api from "./url";

export function login(params) {
  return fetch({
    url: api.serverUrl + '',
    method: 'POST',
    data:params,
  })
}
```

## 使用接口函数
```
import {login} from "../../axios/api";

在方法里调接口
getMessage(){
login().then(res=>{

})
}

```

