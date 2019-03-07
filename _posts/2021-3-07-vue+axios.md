---
title: vue+axios接口请求
date: 2019-3-07 10:58:04
tags: 
    - vue
    - axios
    
categories: vue axios
description: vue+axios接口请求
---


### 在使用Vue搭建项目时，接口请求的配置：
### 全局安装axios：```npm install axios --save```
### 在main.js里配置：```import {api} from './assets/js/api'  window.$api = api;```  ，也可以``` Vue.prototype.$api = api;```.使用window挂载的方式好处在于在页面使用的时候直接是api，使用挂载Vue原型的方式在页面使用的时候前面要加$,即$api
### 在assets/js/api文件里：
```
import axios from 'axios'
let api = api || {};
api.baseUrl = '';
const http = axios.create({
    headers :{
        'Content-Type':'application/json',
    },
    timeout:3000
});
axios.defaults.baseURL = api.baseUrl; //这句话的作用是：如果有这句话，后面写接口得时候不用拼接api.baseUrl，如果没有，后面就是api.baseUrl+''

http.interceptors.request.use(
    config =>{
        config.headers.token = localStorage.getItem('_token');//写在此处防止第一次进去token为空
        if(config.method === 'post'){
            config.data = JSON.stringify(config.data);
        }
        return config;
    },
    error => {
        return Promise.reject(error);
    }
);

http.interceptors.response.use(
    res =>{
        if(res.status === 200){
            return res.data;
        }else{
            return {
                flag:2,
                message:"请求数据失败"
            }
        }
    },
    error => {
        return Promise.reject(error);
    }
);

api.http = http;

//具体的接口
api.login = '';


export {api}; //写在最后

```




