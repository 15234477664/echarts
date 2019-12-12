# echarts
在Vue中使用echarts

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
