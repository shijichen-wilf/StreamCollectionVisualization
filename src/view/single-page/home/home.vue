<template>
  <div>
    <Row :gutter="20" style="margin-top: 10px;">
      <i-col :md="24" :lg="8" style="margin-bottom: 20px;">
        <Card shadow>
          <chart-pie ref="chart-pie" style="height: 300px;" :value="pieData" text="用户访问来源"></chart-pie>
        </Card>
      </i-col>
      <i-col :md="24" :lg="16" style="margin-bottom: 20px;">
        <Card shadow>
          <chart-bar style="height: 300px;" :value="barData" text="每周用户活跃量"/>
        </Card>
      </i-col>
    </Row>
    <Row>
      <Card shadow>
        <example style="height: 310px;"/>
      </Card>
    </Row>
  </div>
</template>

<script>
import { ChartPie, ChartBar } from '_c/charts'
import Example from './example.vue'
import { getRegisters } from '@/api/data'
export default {
  name: 'home',
  components: {
    'chart-pie': ChartPie,
    ChartBar,
    Example
  },
  data () {
    return {
      pieData: [],
      barData: {
        Mon: 13253,
        Tue: 34235,
        Wed: 26321,
        Thu: 12340,
        Fri: 24643,
        Sat: 1322,
        Sun: 1324
      }
    }
  },
  mounted () {
    //
    this.timeTest()
  },
  methods: {
    timeTest () {
      let tmp = []
      getRegisters().then(res => {
        console.log(111)
        tmp = [
          { value: 335, name: '直接访问' },
          { value: 310, name: '邮件营销' },
          { value: 234, name: '联盟广告' },
          { value: 135, name: '视频广告' },
          { value: 1548, name: '搜索引擎' }
        ]
        // this.$refs.ChartPie.setValue(tmp)
        // this.$refs["ChartPie"].setValue(tmp)
        this.$refs['chart-pie'].refresh(tmp)
      })
    }
  }
}
</script>

<style lang="less">
.count-style{
  font-size: 50px;
}
</style>
