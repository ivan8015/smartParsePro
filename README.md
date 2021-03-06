<!--
 * @Author: wangzhichiao<https://github.com/wzc570738205>
 * @Date: 2020-04-15 11:34:04
 * @LastEditors: wangzhichiao<https://github.com/wzc570738205>
 * @LastEditTime: 2020-05-22 10:16:42
 -->

# 智能识别收货地址Pro（支持vue）/省市区街道四级联动（支持省市区县街道/姓名/电话/邮编/身份证号码识别）
### 文档地址：[语雀](https://www.yuque.com/books/share/72418abc-287d-4a67-ae3c-dad10928c631?#)

### 在线预览：[预览地址(请耐心等待加载)](https://wangzc.wang/smartParsePro/)


### 交流Q群：[749539640](https://jq.qq.com/?_wv=1027&k=55bQp1O)

> 地址识别问题请@群主

![image.png](https://s2.ax1x.com/2020/01/02/lYkqdx.png)
## 地址数据来源(数据不对请更新此json)
更新方法：将此json文件内容复制至同名js里的var pcassCode=xxxx;

[pcas-code.json(点击前往)](https://github.com/modood/Administrative-divisions-of-China/blob/master/dist/pcas-code.json)

## 支持以下数据格式
### 注意：地址、姓名、电话、邮编、身份证号码【字母大写】用空格或者特殊字符分开!!

特殊字符(可自行添加)：
```
~!@#$^&*()=|{}':;',\\[\\].<>/?~！@#￥……&*（）——|{}【】‘；：”“’。，、？-

```
 1. 广东省珠海市香洲区盘山路28号幸福茶庄,陈景勇，13593464918
2. 马云，陕西省西安市雁塔区丈八沟街道高新四路高新大都荟  13593464918
3. 陕西省西安市雁塔区丈八沟街道高新四路高新大都荟710061 刘国良 13593464918 211381198512096810
4. 西安市雁塔区丈八沟街道高新四路高新大都荟710061 刘国良 13593464918 211381198512096810
5. 雁塔区丈八沟街道高新四路高新大都荟710061 刘国良 13593464918 211381198512096810
6. 北京市朝阳区姚家园3楼 13593464918 马云
7. 河北省石家庄市新华区中华北大街68号鹿城商务中心6号楼1413室 150-3569-6956 马云
## 不支持的数据格式
陕西省西安市雁塔区丈八沟街道高新四路高新大都荟马云13593464918

## 地址切分规则
1. `省市区(县)街道详细地址`+`电话`+`邮编`+`姓名`+`身份证号码`
## 使用方法

### 1.api调用(5/13上线，可先在dev环境测试)

```
request url：https://wangzc.wang/smAddress

request methods: POST

request payload: 

{
  "address":"广东省珠海市香洲区盘山路28号幸福茶庄,陈景勇，13593464918"
}
response： 

{
    "province":"广东省",
    "provinceCode":"44",
    "city":"珠海市",
    "cityCode":"4404",
    "county":"香洲区",
    "countyCode":"440402",
    "address":"盘山路28号幸福茶庄",
    "name":"陈景勇",
    "phone":"13593464918"
}

```
api使用推荐axios
```
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>

axios({
  method: "post",
  url: "https://wangzc.wang/smAddress",
  data: {
    address: '广东省珠海市香洲区盘山路28号幸福茶庄,陈景勇，13593464918',
  },
}).then(function (res) {});
```

### 2.ES5使用（建议下载demo查看引入js顺序以及调用方法）
```
<script src="js/pcasCode.js"></script>
<script src="js/zipCode.js"></script>
<script src="js/address_parse.js"></script>
//gitee
<script src="http://wzhichao.gitee.io/smartParsePro/js/pcasCode.js"></script>
<script src="http://wzhichao.gitee.io/smartParsePro/js/zipCode.js"></script>
<script src="http://wzhichao.gitee.io/smartParsePro/js/address_parse.js"></script>


smart("陕西省西安市雁塔区丈八沟街道高新四路高新大都荟710061 刘国良 13593464918 211381198512096810")
```
### 3.小程序使用（如需要自行构建后台，json文件在demo/后台json/database_export-sw0HKSJkxA1j.json）
将仓库中的```smartWeChat```文件夹拷贝到项目中```app.js```的同级目录
> 详见smartWeChat=>README.md
[文档地址](https://github.com/wzc570738205/smartParsePro/tree/master/smartWeChat)
### 4.1 vue环境下使用（推荐）
index.html引入js(文件可自行下载部署在自己服务器上)
```
//gitee
<script src="http://wzhichao.gitee.io/smartParsePro/js/pcasCode.js"></script>
<script src="http://wzhichao.gitee.io/smartParsePro/js/zipCode.js"></script>
<script src="http://wzhichao.gitee.io/smartParsePro/js/address_parse.js"></script>
```

xxx.vue（address_parse2.js会暴露全局window方法 smart）
```
mounted() {
  console.log(window.smart('河北省石家庄市新华区中华北大街68号鹿城商务中心6号楼1413室 150-3569-6956 马云'))
}
```
### 4.2[vue环境下使用](https://github.com/wzc570738205/vue-smart-parse) 这种方法会导致打包体积大

```
npm install  vue-smart-parse -d -s
```

```
 // main.js
 import smartParse from 'vue-smart-parse';
 Vue.use(smartParse)
 // App.vue
console.log(this.smartParse('浙江省杭州市西湖区盘山路28号幸福茶庄 陈红 13593464918'));
```


## 生成数据格式
```
{
 zipCode:710061

 province:陕西省

 provinceCode:61

 city:西安市

 cityCode:6101

 county:雁塔区

 countyCode:610113

 street:丈八沟街道

 streetCode:610113007

 address:高新四路高新大都荟

 name:刘国良

 phone:13593464918

 idCard:211381198512096810
}
```


##### 地址数据来源：[中华人民共和国行政区划](https://github.com/modood/Administrative-divisions-of-China)
##### 邮编数据来源：[中华人民共和国邮编](https://github.com/xieranmaya/china-city-area-zip-data/blob/master/china-city-area-zip.json)

#### 请作者喝杯咖啡☕️
![](http://cdn.wangzc.wang/uPic/cDQzFD.jpg)


