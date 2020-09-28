<template>
    <div>
        <transition enter-active-class="animate__animated animate__jackInTheBox" leave-active-class="animate__animated animate__fadeOutRightBig">
            <div ref='countCharts'
                style="height: 200px;width: 370px;"
                class=""></div>
        </transition>
        <transition enter-active-class="animate__animated animate__fadeIn animate__delay-1s" leave-active-class="animate__animated animate__fadeOut">
            <div ref="caseAboutYear"
                style="height: 200px;width: 370px;"></div>
        </transition>
    </div>
</template>
<script>
import echarts from "echarts";
import { dataAll } from "./data"
export default {
    name: "chartBeautiful",
    data () {
        return {
            caseStartWhichTime: [{ CaseAddNotClosedNumber: 5, CaseAddClosedNumber: 7, CaseAddNumber: 12, time: "2019-10" }
                , { CaseAddNotClosedNumber: 5, CaseAddClosedNumber: 6, CaseAddNumber: 11, time: "2019-11" }
                , { CaseAddNotClosedNumber: 39, CaseAddClosedNumber: 4, CaseAddNumber: 43, time: "2019-12" }
                , { CaseAddNotClosedNumber: 9, CaseAddClosedNumber: 2, CaseAddNumber: 11, time: "2020-01" }
                , { CaseAddNotClosedNumber: 0, CaseAddClosedNumber: 0, CaseAddNumber: 0, time: "2020-02" }
                , { CaseAddNotClosedNumber: 10, CaseAddClosedNumber: 1, CaseAddNumber: 11, time: "2020-03" }
                , { CaseAddNotClosedNumber: 3, CaseAddClosedNumber: 1, CaseAddNumber: 4, time: "2020-04" }
                , { CaseAddNotClosedNumber: 0, CaseAddClosedNumber: 0, CaseAddNumber: 0, time: "2020-05" }
                , { CaseAddNotClosedNumber: 19, CaseAddClosedNumber: 0, CaseAddNumber: 19, time: "2020-06" }
                , { CaseAddNotClosedNumber: 5, CaseAddClosedNumber: 4, CaseAddNumber: 9, time: "2020-07" }
                , { CaseAddNotClosedNumber: 25, CaseAddClosedNumber: 0, CaseAddNumber: 25, time: "2020-08" }
                , { CaseAddNotClosedNumber: 39, CaseAddClosedNumber: 5, CaseAddNumber: 45, time: "2020-09" }],
            caseBigData: {
                caseAgeAnalysisMap: {
                    "18岁": 12,
                    "18-35岁": 237,
                    "35-50岁": 166,
                    "50-70岁": 77,
                    "70+岁": 1
                }
            }
        }
    },
    mounted () {
        this.countCharts();
        this.caseAboutYearChart();
    },
    methods: {
        caseAboutYearChart () {
            let myChartDiv = this.$refs.caseAboutYear;
            if (myChartDiv) {
                let myChart = echarts.init(this.$refs.caseAboutYear);
                let data = [];
                let dataX = [];
                for (let i in this.caseBigData.caseAgeAnalysisMap) {
                    dataX.push(i);
                    data.push(this.caseBigData.caseAgeAnalysisMap[i]);
                }
                function sortNumber (a, b) {
                    return a - b
                }
                let dark = [...data]; //阴影部分的高度为最高数据
                let darkNum = dark.sort(sortNumber)[dark.length - 1];
                let dataShadow = []; //阴影部分各项数据，同一值
                for (let i = 0; i < dark.length; i++) {
                    dataShadow.push(darkNum)
                }
                let option = {
                    tooltip: {
                        axisPointer: {
                            type: 'none',
                            label: {
                                backgroundColor: 'rgba(0,0,0,0)',
                                color: '#50ebff',
                            }
                        },
                        //触发类型：坐标轴触发
                        position: 'left',
                        trigger: 'axis',
                        backgroundColor: 'rgba(25,38,74,0.5)',//通过设置rgba调节背景颜色与透明度
                        color: 'black',
                        borderWidth: '1',
                        borderColor: '#50ebff',
                        borderRadius: 'none',
                        textStyle: {
                            color: '#aad2dc',
                            fontFamily: 'LCDD'
                        },
                        formatter: function (params) {
                            let str = `
                            <div>
                                <div>${params[0].axisValue}</div>
                                <span style="width: 4px;height: 4px;display: inline-block;border: 3px solid #00b4ff;border-radius: 50%;"></span>&nbsp;&nbsp;<span style="color: #aaa;">人数：</span> ${params[1].value}
                            </div>`
                            return str
                        },
                    },
                    xAxis: {
                        data: dataX,
                        axisLabel: { //x坐标轴文字颜色
                            textStyle: {
                                color: '#474b53'
                            }
                        }
                    },
                    yAxis: {
                        axisLabel: { //y轴文字颜色
                            textStyle: {
                                color: '#474b53'
                            }
                        },
                        axisLine: {
                            show: false
                        },
                        axisTick: {
                            show: false
                        },
                        axisLabel: {
                            color: '#474b53'
                        },
                        splitLine: {
                            lineStyle: {
                                color: '#2e3035',
                                type: 'dashed'
                            }
                        }
                    },
                    grid: {
                        left: '3%',
                        right: '3%',
                        top: '10%',
                        bottom: '15%',
                        containLabel: true,
                        borderColor: 'red'
                    },
                    series: [
                        { //阴影
                            type: 'bar',
                            itemStyle: {
                                color: '#474b53',
                                barBorderRadius: 5
                            },
                            barGap: '-100%',
                            barCategoryGap: '90%',
                            data: dataShadow,
                            animation: false
                        },
                        {
                            type: 'bar',
                            itemStyle: {
                                color: new echarts.graphic.LinearGradient(
                                    0, 0, 0, 1,
                                    [
                                        { offset: 0, color: '#adfcf1' },
                                        { offset: 0.5, color: '#00b4ff' },
                                        { offset: 1, color: '#00b4ff' }
                                    ]
                                ),
                                barBorderRadius: 5
                            },
                            emphasis: {
                                itemStyle: {
                                    color: new echarts.graphic.LinearGradient(
                                        0, 0, 0, 1,
                                        [
                                            { offset: 0, color: '#00b4ff' },
                                            { offset: 0.7, color: '#2378f7' },
                                            { offset: 1, color: '#83bff6' }
                                        ]
                                    )
                                }
                            },
                            data: data
                        }
                    ]
                };
                myChart.clear();
                setTimeout(() => {
                    myChart.setOption(option, true);
                }, 1000)
            }
        },
        countCharts () {//案件发生分析画图
            let myChart = echarts.init(this.$refs.countCharts);
            if (myChart) {
                let dataX = [];
                let dataSeries1 = [];
                let dataSeries2 = [];
                let dataSeries3 = [];
                this.caseStartWhichTime.map(item => {
                    dataX.push(item.time);
                    dataSeries1.push(item.CaseAddNumber);
                    dataSeries2.push(item.CaseAddClosedNumber);
                    dataSeries3.push(item.CaseAddNotClosedNumber);
                })

                let option = {
                    tooltip: {
                        axisPointer: {
                            type: 'none',
                            label: {
                                backgroundColor: 'rgba(0,0,0,0)',
                                color: '#50ebff',
                            }
                        },
                        //触发类型：坐标轴触发
                        position: 'left',
                        trigger: 'axis',
                        backgroundColor: 'rgba(25,38,74,0.5)',//通过设置rgba调节背景颜色与透明度
                        color: 'black',
                        borderWidth: '1',
                        borderColor: '#50ebff',
                        borderRadius: 'none',
                        textStyle: {
                            color: '#aad2dc',
                            fontFamily: 'LCDD'
                        }
                        //extraCssText:'background:rgba(0, 0, 0, 0.5);'
                    },
                    grid: {
                        left: '0',
                        right: '3%',
                        top: '10%',
                        bottom: '15%',
                        containLabel: true,
                        borderColor: 'red'
                    },
                    xAxis: {
                        show: false,
                        type: 'category',
                        boundaryGap: false,
                        axisLabel: {
                            color: '#2c517f'
                        },
                        axisLine: {
                            lineStyle: {
                                color: '#212e50'
                            }
                        },
                        data: dataX
                    },
                    yAxis: {
                        show: false,
                        type: 'value',
                        axisLine: {
                            show: false
                        },
                        axisTick: {
                            show: false
                        },
                        axisLabel: {
                            color: '#2c517f'
                        },
                        splitLine: {
                            lineStyle: {
                                color: '#212e50'
                            }
                        }
                    },
                    color: ['#1744fd', '#36beff', '#ffb965'],
                    series: [
                        {
                            name: '新增',
                            type: 'line',
                            smooth: true,//线是直的还是弯的
                            symbol: 'none',//有没有线上那个点
                            areaStyle: {
                                color: {
                                    type: 'linear',
                                    x: 0,
                                    x2: 0,
                                    y: 0,
                                    y2: 1,
                                    colorStops: [{
                                        offset: 0, color: 'rgba(23,68,235,1)' // 0% 处的颜色
                                    }, {
                                        offset: 1, color: 'rgba(23,68,235,0.3)' // 100% 处的颜色
                                    }],
                                }
                            },
                            data: dataSeries1
                        },
                        {
                            name: '已侦破',
                            type: 'line',
                            smooth: true,//线是直的还是弯的
                            symbol: 'none',//有没有线上那个点
                            areaStyle: {
                                color: {
                                    type: 'linear',
                                    x: 0,
                                    x2: 0,
                                    y: 0,
                                    y2: 1,
                                    colorStops: [{
                                        offset: 0, color: 'rgb(54 190 255 / 1)' // 0% 处的颜色
                                    }, {
                                        offset: 1, color: 'rgb(54 190 255 / 0.3)' // 100% 处的颜色
                                    }],
                                }
                            },
                            data: dataSeries2
                        },
                        {
                            name: '未侦破',
                            type: 'line',
                            smooth: true, //线是直的还是弯的
                            symbol: 'none',//有没有线上那个点
                            areaStyle: {
                                color: {
                                    type: 'linear',
                                    x: 0,
                                    x2: 0,
                                    y: 0,
                                    y2: 1,
                                    colorStops: [{
                                        offset: 0, color: 'rgba(255,185,101,1)' // 0% 处的颜色
                                    }, {
                                        offset: 1, color: 'rgba(255,185,101,0.3)' // 100% 处的颜色
                                    }],
                                }
                            },
                            data: dataSeries3
                        }
                    ]
                }
                myChart.clear()
                setTimeout(() => {
                    myChart.setOption(option, true);
                }, 1000)
            }
        },
    }
};
</script>
