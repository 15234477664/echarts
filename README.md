# echarts(在Vue中使用echarts)

## 先npm安装echarts
```js
npm install echarts --save
```
## 在main.js中
```js
import echarts from 'echarts'
Vue.prototype.$echarts = echarts
```
## 在Echarts.vue中
```vue
<div id="myChart" :style="{width: '300px', height: '300px'}"></div>

export default {
  name: 'hello',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  mounted(){
    this.drawLine();
  },
  methods: {
    drawLine(){
        // 基于准备好的dom，初始化echarts实例
        let myChart = this.$echarts.init(document.getElementById('myChart'))
        // 绘制图表
        myChart.setOption({
            title: { text: '在Vue中使用echarts' },
            tooltip: {},
            xAxis: {
                data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
            },
            yAxis: {},
            series: [{
                name: '销量',
                type: 'bar',
                data: [5, 20, 36, 10, 10, 20]
            }]
        });
    }
  }
}
```
### 注意：我们要在mounted生命周期函数中实例化echarts对象。因为我们要确保dom元素已经挂载到页面中

# vue 中添加字符云
## 首先安装
```js
npm install echarts-wordcloud
```
## 在main.js中
```js
import 'echarts-wordcloud/dist/echarts-wordcloud'
```
```html
<template>
    <div id="wordCloud" :style="{width: '100%', height: '100%'}"></div>
</template>
 ```
 ```js
 <script>
export default {
    data(){
        return{
            
        }
    },
    mounted(){
        this.drawCloud()
    },
    methods:{
        drawCloud(){
            let wordCloud = this.$echarts.init(document.getElementById('wordCloud'));
            function createRandomItemStyle() {
                return {
                    normal: {
                        color: 'rgb(' + [
                            Math.round(Math.random() * 160),
                            Math.round(Math.random() * 160),
                            Math.round(Math.random() * 160)
                        ].join(',') + ')'
                    }
                };
            }
            let text = ['Sam S Club','Macys','Amy Schumer','Jurassic World','Charter Communications','Chick Fil A','Planet Fitness','Pitch Perfect','Express','Home','Johnny Depp','Lena Dunham','Lewis Hamilton','KXAN','Mary Ellen Mark','Farrah Abraham','Rita Ora','Serena Williams','NCAA baseball tournament','Point Break']
            let data = [];
            for(var i = 0; i < text.length; i++){
                let obj = {};
                obj.name = text[i];
                obj.value = Math.random()*10000;
                data.push(obj)
            }
            console.log(data)
            let option = {
                title: {
                    text: 'Google Trends',
                    link: ''
                },
                tooltip: {
                    show: true
                },
                series: [{
                    name: 'Google Trends',
                    type: 'wordCloud',
                    size: ['80%', '80%'],
                    textRotation : [0, 45, 90, -45],
                    textPadding: 0,
                    autoSize: {
                        enable: true,
                        minSize: 14
                    },
                     textStyle: {//文字样式设置
                        normal: {
                            color: function() {//颜色
                                return 'rgb(' + [//返回随机生成的颜色
                                    Math.round(Math.random() * 160),
                                    Math.round(Math.random() * 160),
                                    Math.round(Math.random() * 160)
                                ].join(',') + ')';
                            }
                        },
                        emphasis: {//鼠标划入样式
                            shadowBlur: 10,//文字阴影模糊度
                            shadowColor: '#333'//文字阴影颜色
                        }
                    },
                    data:data
                }]
            }
            wordCloud.setOption(option)
        }
        
    }
}
</script>
 ```
