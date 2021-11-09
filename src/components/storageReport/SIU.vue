<template>
  <div class="com-chart" ref="chartRef"></div>
</template>
<script>
export default {
  data() {
    return {
      chartInstance: null, // echart图表实例
      chartData: null, // 图表展示数据
      ChartOptionName: '交换机接口使用率图表配置',
      chartOption: '', // 图表配置信息option
      optionList: [], //故障分布图保存的历史配置信息
    }
  },
  props: ['currentWeek', 'newDataAndScript'],
  watch: {
    // 监听父组件传来的新周数
    currentWeek: {
      handler: function(newVal, oldVal) {
        // this.getData()
        // this.initChart()
        // this.sendOption()
      },
      immediate: true,
    },
    newDataAndScript: {
      deep: true,
      handler: function(val) {
        // if (val.data.length === 0) {
        //   this.changeChart(val.newEditorContent, this.chartData)
        // } else {
        //   this.changeChart(val.newEditorContent, val.data)
        // }
        this.changeChart(val.newEditorContent, val.data)
      },
    },
  },
  mounted() {
    this.initChart()
    //向父组件发送图表配置名称
    this.$emit('sendChartOptionName', this.ChartOptionName)
    window.addEventListener('resize', this.screenAdapter)
    // 在页面加载完成时候，主动进行屏幕适配
    this.screenAdapter()
  },

  methods: {
    //   初始化图表
    initChart() {
      // 初始化echart实例
      let myChart = this.$echarts.init(this.$refs.chartRef)
      let option
      let data = [
        {
          名称: '接口1',
          '低于50%使用率': 0.3,
          '使用率50%~80%': 0.4,
          '使用率80%以上': 0.3,
        },
        {
          名称: '接口2',
          '低于50%使用率': 0.2,
          '使用率50%~80%': 0.1,
          '使用率80%以上': 0.7,
        },
        {
          名称: '接口3',
          '低于50%使用率': 0.25,
          '使用率50%~80%': 0.35,
          '使用率80%以上': 0.4,
        },
        {
          名称: '接口4',
          '低于50%使用率': 0.1,
          '使用率50%~80%': 0.8,
          '使用率80%以上': 0.1,
        },
        {
          名称: '接口5',
          '低于50%使用率': 0.6,
          '使用率50%~80%': 0.3,
          '使用率80%以上': 0.1,
        },
        {
          名称: '接口6',
          '低于50%使用率': 0.55,
          '使用率50%~80%': 0.35,
          '使用率80%以上': 0.1,
        },
        {
          名称: '接口7',
          '低于50%使用率': 0.9,
          '使用率50%~80%': 0.05,
          '使用率80%以上': 0.05,
        },
        {
          名称: '接口8',
          '低于50%使用率': 0.48,
          '使用率50%~80%': 0.12,
          '使用率80%以上': 0.4,
        },
        {
          名称: '接口9',
          '低于50%使用率': 0.22,
          '使用率50%~80%': 0.48,
          '使用率80%以上': 0.3,
        },
        {
          名称: '接口10',
          '低于50%使用率': 0.3,
          '使用率50%~80%': 0.5,
          '使用率80%以上': 0.2,
        },
        {
          名称: '接口11',
          '低于50%使用率': 0.3,
          '使用率50%~80%': 0.4,
          '使用率80%以上': 0.3,
        },
        {
          名称: '接口12',
          '低于50%使用率': 0.2,
          '使用率50%~80%': 0.1,
          '使用率80%以上': 0.7,
        },
        {
          名称: '接口13',
          '低于50%使用率': 0.25,
          '使用率50%~80%': 0.35,
          '使用率80%以上': 0.4,
        },
        {
          名称: '接口14',
          '低于50%使用率': 0.1,
          '使用率50%~80%': 0.8,
          '使用率80%以上': 0.1,
        },
        {
          名称: '接口15',
          '低于50%使用率': 0.6,
          '使用率50%~80%': 0.3,
          '使用率80%以上': 0.1,
        },
        {
          名称: '接口16',
          '低于50%使用率': 0.55,
          '使用率50%~80%': 0.35,
          '使用率80%以上': 0.1,
        },
        {
          名称: '接口17',
          '低于50%使用率': 0.9,
          '使用率50%~80%': 0.05,
          '使用率80%以上': 0.05,
        },
        {
          名称: '接口18',
          '低于50%使用率': 0.48,
          '使用率50%~80%': 0.12,
          '使用率80%以上': 0.4,
        },
        {
          名称: '接口19',
          '低于50%使用率': 0.22,
          '使用率50%~80%': 0.48,
          '使用率80%以上': 0.3,
        },
        {
          名称: '接口20',
          '低于50%使用率': 0.3,
          '使用率50%~80%': 0.5,
          '使用率80%以上': 0.2,
        },
        {
          名称: '接口21',
          '低于50%使用率': 0.3,
          '使用率50%~80%': 0.5,
          '使用率80%以上': 0.2,
        },
        {
          名称: '接口22',
          '低于50%使用率': 0.3,
          '使用率50%~80%': 0.5,
          '使用率80%以上': 0.2,
        },
        {
          名称: '接口23',
          '低于50%使用率': 0.3,
          '使用率50%~80%': 0.5,
          '使用率80%以上': 0.2,
        },
        {
          名称: '接口24',
          '低于50%使用率': 0.3,
          '使用率50%~80%': 0.5,
          '使用率80%以上': 0.2,
        },
        {
          名称: '接口25',
          '低于50%使用率': 0.3,
          '使用率50%~80%': 0.5,
          '使用率80%以上': 0.2,
        },
        {
          名称: '接口26',
          '低于50%使用率': 0.3,
          '使用率50%~80%': 0.5,
          '使用率80%以上': 0.2,
        },
        {
          名称: '接口27',
          '低于50%使用率': 0.3,
          '使用率50%~80%': 0.5,
          '使用率80%以上': 0.2,
        },
        {
          名称: '接口28',
          '低于50%使用率': 0.3,
          '使用率50%~80%': 0.5,
          '使用率80%以上': 0.2,
        },
        {
          名称: '接口29',
          '低于50%使用率': 0.3,
          '使用率50%~80%': 0.5,
          '使用率80%以上': 0.2,
        },
        {
          名称: '接口30',
          '低于50%使用率': 0.3,
          '使用率50%~80%': 0.5,
          '使用率80%以上': 0.2,
        },
        {
          名称: '接口31',
          '低于50%使用率': 0.3,
          '使用率50%~80%': 0.5,
          '使用率80%以上': 0.2,
        },
        {
          名称: '接口32',
          '低于50%使用率': 0.3,
          '使用率50%~80%': 0.5,
          '使用率80%以上': 0.2,
        },
        {
          名称: '接口33',
          '低于50%使用率': 0.3,
          '使用率50%~80%': 0.5,
          '使用率80%以上': 0.2,
        },
        {
          名称: '接口34',
          '低于50%使用率': 0.3,
          '使用率50%~80%': 0.5,
          '使用率80%以上': 0.2,
        },
        {
          名称: '接口35',
          '低于50%使用率': 0.3,
          '使用率50%~80%': 0.5,
          '使用率80%以上': 0.2,
        },
        {
          名称: '接口36',
          '低于50%使用率': 0.3,
          '使用率50%~80%': 0.5,
          '使用率80%以上': 0.2,
        },
        {
          名称: '接口37',
          '低于50%使用率': 0.3,
          '使用率50%~80%': 0.5,
          '使用率80%以上': 0.2,
        },
        {
          名称: '接口38',
          '低于50%使用率': 0.3,
          '使用率50%~80%': 0.5,
          '使用率80%以上': 0.2,
        },
        {
          名称: '接口39',
          '低于50%使用率': 0.3,
          '使用率50%~80%': 0.5,
          '使用率80%以上': 0.2,
        },
        {
          名称: '接口40',
          '低于50%使用率': 0.3,
          '使用率50%~80%': 0.5,
          '使用率80%以上': 0.2,
        },
        {
          名称: '接口41',
          '低于50%使用率': 0.3,
          '使用率50%~80%': 0.5,
          '使用率80%以上': 0.2,
        },
        {
          名称: '接口42',
          '低于50%使用率': 0.3,
          '使用率50%~80%': 0.5,
          '使用率80%以上': 0.2,
        },
        {
          名称: '接口43',
          '低于50%使用率': 0.3,
          '使用率50%~80%': 0.5,
          '使用率80%以上': 0.2,
        },
        {
          名称: '接口44',
          '低于50%使用率': 0.3,
          '使用率50%~80%': 0.5,
          '使用率80%以上': 0.2,
        },
        {
          名称: '接口45',
          '低于50%使用率': 0.3,
          '使用率50%~80%': 0.5,
          '使用率80%以上': 0.2,
        },
        {
          名称: '接口46',
          '低于50%使用率': 0.3,
          '使用率50%~80%': 0.5,
          '使用率80%以上': 0.2,
        },
        {
          名称: '接口47',
          '低于50%使用率': 0.3,
          '使用率50%~80%': 0.5,
          '使用率80%以上': 0.2,
        },
        {
          名称: '接口48',
          '低于50%使用率': 0.3,
          '使用率50%~80%': 0.5,
          '使用率80%以上': 0.2,
        },
      ]

      for (let rec of data) {
        rec['低于50%使用率'] = Math.random() * 0.2 + 0.6
        rec['使用率50%~80%'] =
          Math.random() * (0.8 - rec['低于50%使用率']) + 0.2
        rec['使用率80%以上'] = 1 - rec['低于50%使用率'] - rec['使用率50%~80%']
      }

      option = {
        title: {
          text: '核心应用SAN交换机 端口使用情况',
          left: '1%',
        },
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            // Use axis to trigger tooltip
            type: 'shadow', // 'shadow' as default; can also be 'line' or 'shadow'
          },
        },
        legend: {},
        grid: {
          left: '3%',
          right: '4%',
          bottom: '3%',
          containLabel: true,
        },
        tooltip: {
          formatter: param => {
            // return param.seriesName + ' <br/>'
            //     + param.value["存储"] + ' <br/>'
            //     + param.value["日期"] + ' <br/>';
            return `${param.value['名称']} <br/> 
      低于50%时长占比: ${(param.value['低于50%使用率'] * 100).toFixed(0)}% <br/>
      50%~80%时长占比: ${(param.value['使用率50%~80%'] * 100).toFixed(0)}% <br/>
      高于80%时长占比: ${(param.value['使用率80%以上'] * 100).toFixed(0)}%`
          },
        },
        dataset: [
          // x是按 (当前日期-最小日期) / (最大日期 - 最小日期) 的一个比例得出的位置
          // y是按 (当前日期所在星期) + (存储的序号下标 x 7) 得出哪个存储哪个星期几发生的故障
          {
            dimensions: [
              '名称',
              '低于50%使用率',
              '使用率50%~80%',
              '使用率80%以上',
            ],
            source: data,
          },
        ],

        xAxis: {
          type: 'value',
          axisLabel: {
            formatter: param => {
              return `${param * 100}%`
            },
          },
        },
        yAxis: {
          type: 'category',
        },
        series: [
          {
            type: 'bar',
            stack: 'total',
            seriesLayoutBy: 'row',
            // emphasis: {
            //   focus: 'series'
            // },
            // label: {
            //   show: true,
            // },
          },
          {
            type: 'bar',
            stack: 'total',
            seriesLayoutBy: 'row',
            // emphasis: {
            //   focus: 'series'
            // },
            // label: {
            //   show: true,
            // },
          },
          {
            type: 'bar',
            stack: 'total',
            seriesLayoutBy: 'row',
            // emphasis: {
            //   focus: 'series'
            // },
            // label: {
            //   show: true,
            // },
          },
        ],
      }

      myChart.setOption(option)
      this.chartInstance = myChart
      // 将option赋值给chartOption，此时chartOption内容是一个对象
      this.chartOption = option
    },
    // 更改图表
    changeChart(script,data) {
      // 用echarts时，如果不存在DOM，就会报错，处理方法先检查是否DOM存在：
      if (this.$refs.chartRef == null) {
        return
      }
      // 用echarts时，如果存在DOM，就会报存在警告，处理方法删除DOM：
      this.$echarts.dispose(this.$refs.chartRef)
      try {
        data = JSON.stringify(data)
        let func = new Function(
          'echarts',
          `const ROOT_PATH = 'https://cdn.jsdelivr.net/gh/apache/echarts-website@asf-site/examples';var option;let myChart = echarts.init(this.$refs.chartRef);let data;data = ${data};` +
            script +
            `myChart.clear();option && myChart.setOption(option);`
        ).bind(this)
        func(this.$echarts)
      } catch (error) {
        console.log(error);
        this.$message({
          message: '数据或代码出错',
          type: 'error',
        })
      }
    },
    // 当浏览器大小发生变化时候，调用方法完成屏幕适配
    screenAdapter() {
      const titleFontSize = (this.$refs.chartRef.offsetWidth / 100) * 1.5
      // 和分辨率大小相关的配置项
      const adapterOption = {
        title: {
          textStyle: {
            fontSize: titleFontSize,
          },
        },
      }
      this.chartInstance.setOption(adapterOption)
      // 手动调用图表对象的resize才能产生效果
      this.chartInstance.resize()
    },
  },
}
</script>
<style lang="less" scoped></style>
