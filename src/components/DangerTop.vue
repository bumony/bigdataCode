<template>
  <div class="com-container">
    <div class="com-chart"
         ref="dangertop_ref"></div>
  </div>

</template>

<script>
export default {
  data () {
    return {
      chartInstance: null
    }
  },
  mounted () {
    this.initChart()
    this.getData()
    window.addEventListener('resize', this.screenAdapter)
    this.screenAdapter()
  },
  destroyed () {
    clearInterval(this.timeId)
    window.removeEventListener('resize', this.screenAdapter)
  },
  methods: {
    // 初始化echarts
    initChart () {
      this.chartInstance = this.$echarts.init(this.$refs.dangertop_ref, 'chalk')
      // 图表初始化
      const initOption = {
        title: {
          text: '▍企业危险驾驶员排名TOP10',
          left: 20,
          top: 20
        },
        legend: {
          data: ['安全指标', '经济指标']
        },
        xAxis: {
          type: 'category',
          max: 10,
          inverse: 'ture'
        },
        yAxis: {
          type: 'value'
        },
        series: [
          {
            realtimeSort: true,
            name: '安全指标',
            type: 'bar',
            stack: '指标',
            emphasis: {
              focus: 'series'
            }
          },
          {
            name: '经济指标',
            type: 'bar',
            stack: '指标',
            emphasis: {
              focus: 'series'
            }
          }
        ]
      }
      this.chartInstance.setOption(initOption)
    },
    getData () {
      this.updateChat()
    },
    updateChat () {
      const dataOption = {

        xAxis: {
          data: ['小红', '小刚', '小明', '小陈', '小李', '小许', '小金', '小赵', '小王', '小芭比', 'chen']
        },
        series: [
          {
            data: [55, 60, 16, 34, 42, 34, 12, 26, 46, 10, 73]
          },
          {
            data: [340, 130, 123, 334, 233, 175, 289, 312, 123, 89, 243]
          }
        ]
      }
      this.chartInstance.setOption(dataOption)
    },
    screenAdapter () {
      // this.$refs.drivertop_ref.offsetWidth
      const titleFontSize = this.$refs.dangertop_ref.offsetWidth / 100 * 3.6
      console.log(titleFontSize)
      const adapterOption = {
        tooltip: {
          axisPointer: {
            lineStyle: {
              width: titleFontSize
            }
          }
        },
        title: {
          textStyle: {
            fontSize: titleFontSize * 0.5
          }
        },
        series: [
          {
            barWidth: titleFontSize * 1.7
          },
          {
            barWidth: titleFontSize * 1.7
          }
        ]
      }
      this.chartInstance.setOption(adapterOption)
      this.chartInstance.resize()
    }
  }
}
</script>

<style>
</style>
