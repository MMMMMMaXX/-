## 在Vue项目中使用第三方组件库

## elementUI

vue add element

## Vant

vue add vant

## ECharts

**1、通过npm获取echarts**

```
npm install echarts --save
```

**2、在vue项目中引入echarts**

在main.js中添加下面两行代码

**main.js**

```
import * as echarts from 'echarts'
Vue.prototype.$echarts = echarts
```

【注释】：`import * as echarts from 'echarts'` 引入echarts后，不能全局使用echarts,所以通过`Vue.prototype` 将echarts保存为全局变量。原则上`$echarts`可以为任意变量名。

**3、新建Echarts.vue 文件**

- 在template中添加一个存放echarts 的'div'容器
- 添加myEcharts()方法，将官方文档中script内容复制到myEcharts()中
- 修改echarts.init()为this.$echarts.init() [因为上面第二步，将echarts保存到全局变量$echarts中]
- 在mounted中调用myEcharts()方法

**Echarts.vue**

```vue
<template>
  <div class="Echarts">
    <div id="main" style="width: 600px;height:400px;"></div>
  </div>
</template>

<script>
export default {
  name: 'Echarts',
  methods:{
	  myEcharts(){
		  // 基于准备好的dom，初始化echarts实例
		  var myChart = this.$echarts.init(document.getElementById('main'));

		  // 指定图表的配置项和数据
		  var option = {
			  title: {
				  text: 'ECharts 入门示例'
			  },
			  tooltip: {},
			  legend: {
				  data:['销量']
			  },
			  xAxis: {
				  data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
			  },
			  yAxis: {},
			  series: [{
				  name: '销量',
				  type: 'bar',
				  data: [5, 20, 36, 10, 10, 20]
			  }]
		  };

		  // 使用刚指定的配置项和数据显示图表。
		  myChart.setOption(option);
		  }
  },
  mounted() {
  	this.myEcharts();
  }
}
</script>

<style>

</style>
```

