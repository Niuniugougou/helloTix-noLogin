<template>
    <d2-container>
        <div ref="mapDiv"
             style="width:100%;height: 100%;"></div>
    </d2-container>
</template>
<script>
import echarts from "echarts";
import geoJson from "@/components/webs/echartsMap/common/mapData"
import mapPoint from "@/components/webs/echartsMap/common/mapPoint"
// import mapPointData from '@/components/webs/echartsMap/common/mapPointData'
export default {
    data () {
        return {

        }
    },
    mounted() {
        this.mapInit();
    },
    methods: {
        mapInit () {
            // 地图上的数据为假数据，所需的数据由自己处理放入就可使用
            let myChartDiv = this.$refs.mapDiv;
            if (myChartDiv) {
                let myChart = echarts.init(myChartDiv);
                echarts.registerMap('chengdu', geoJson);
                let option = {
                    title: {
                        text: '成都市旧地图（有新成都geojson请发给我^_^!）',
                        x: 'center',
                        textStyle: {
                            color: '#000'
                        }
                    },
                    tooltip: { //提示框组件。
                        trigger: 'item', //数据项图形触发，主要在散点图，饼图等无类目轴的图表中使用。
                        formatter: function (data) {
                            let str = `<div><span style="width: 4px;height: 4px; background: #f2ae5d;display: inline-block;border: 3px solid #f2ae5d;border-radius: 50%;"></span>&nbsp;&nbsp;<span style="color: #aaa;">案发数：</span> ${data.data.num}</div> <br/>
                        <span style="width: 4px;height: 4px; background: #f2ae5d;display: inline-block;border: 3px solid #f2ae5d;border-radius: 50%;"></span>&nbsp;&nbsp;<span style="color: #aaa;">已侦破：</span> ${data.data.already}`
                            return str
                        },
                        backgroundColor: 'rgb(37 41 53 / 0.8)',
                        borderWidth: 1,
                        borderColor: 'rgb(37 41 53 / 0.8)',
                        padding: 10,
                        textStyle: {
                            fontSize: '24px',
                            color: '#fff',
                        },
                        extraCssText: 'width: 210px;height: 80px;',
                        borderRadius: 5
                    },
                    geo: {
                        show: true,
                        map: 'chengdu',
                        roam: false,
                        itemStyle: {
                            normal: {
                                areaColor: '#2d3443',
                                shadowColor: 'rgba(0,0,0,0.6)',
                                shadowOffsetX: 25,
                                shadowOffsetY: 25,
                                shadowBlur: 15
                            },
                        },
                    },
                    visualMap: //地图背景色根据数据自动变色
                        [{
                            x: 'left',
                            y: 'center',
                            seriesIndex: [0],
                            show: false,
                            min: 0,
                            max: 400,
                            text: ['High', 'Low'],
                            realtime: false,
                            calculable: false,
                            // color: ['#2d3443', '#4a5365'], //根据数据量地图变色，使用inRange会覆盖圆圈的颜色
                            textStyle: {
                                color: '#7986a1'
                            },
                            inRange: {
                                color: ['#2d3443', '#4a5365']
                            }
                        }],
                    series: [
                        {
                            name: `地区：`,
                            type: 'map',
                            zoom: 1.1,
                            roam: false, //是否开启鼠标缩放和平移
                            label: {
                                normal: {
                                    show: true,
                                    textStyle: {
                                        color: '#7986a1'
                                    }
                                },
                                emphasis: {
                                    textStyle: {
                                        color: '#fff' //移入文字颜色
                                    }
                                }
                            },
                            itemStyle: {
                                normal: {
                                    borderColor: '#474b53', //边框颜色
                                    borderWidth: 1,
                                    areaColor: '#545c6f'
                                },
                                emphasis: { //是图形在高亮状态下的样式,比如在鼠标悬浮或者图例联动高亮时
                                    areaColor: '#fabb49',
                                    borderWidth: 0,
                                    color: 'green'
                                }
                            },
                            map: 'chengdu',
                            data: mapPoint
                        },
                        {
                            type: 'effectScatter',
                            coordinateSystem: 'geo',
                            showEffectOn: 'render',
                            symbolSize: function (value, data) {
                                return data.data.num/100;  //计算圈大小
                            },
                            rippleEffect: {
                                period: 15,
                                scale: 4,
                                brushType: 'fill'
                            },
                            hoverAnimation: false,
                            itemStyle: {
                                normal: {
                                    color: '#ffb965',
                                    shadowBlur: 10,
                                    shadowColor: '#333'
                                }
                            },
                            data: mapPoint
                        }
                    ]
                };
                this.$nextTick(() => {
                    myChart.setOption(option);
                })
            }
        },
    }
}
</script>