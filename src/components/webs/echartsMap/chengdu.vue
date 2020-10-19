<template>
    <d2-container>
        <div ref="mapDiv"
             style="width:100%;height: 100%;"></div>
    </d2-container>
</template>
<script>
import echarts from "echarts";
// import geoJson from "@/components/webs/echartsMap/common/mapData"
import geoJson from "@/components/webs/echartsMap/common/cdNew.js"
import mapPoint from "@/components/webs/echartsMap/common/mapPoint"
export default {
    name: 'chengduMap',
    mounted () {
        this.mapInit();
    },
    data () {
        return {
            caseBigData: {
                caseDistrictStatisticsDtoList: [{
                    CaseClosedNumber: 27,
                    CaseNotClosedNumber: 130,
                    caseCountAddNumber: 0,
                    caseCountNumber: 157,
                    caseDistrictId: "510108",
                    fullName: "成华区",
                    lat: 30.65993,
                    lng: 104.10193
                },
                {
                    CaseClosedNumber: 0,
                    CaseNotClosedNumber: 3,
                    caseCountAddNumber: 0,
                    caseCountNumber: 3,
                    caseDistrictId: "510104",
                    fullName: "锦江区",
                    lat: 30.65614,
                    lng: 104.08347
                },
                {
                    CaseClosedNumber: 0,
                    CaseNotClosedNumber: 24,
                    caseCountAddNumber: 0,
                    caseCountNumber: 24,
                    caseDistrictId: "510181",
                    fullName: "都江堰市",
                    lat: 30.99825,
                    lng: 103.61941
                },
                {
                    CaseClosedNumber: 0,
                    CaseNotClosedNumber: 1,
                    caseCountAddNumber: 0,
                    caseCountNumber: 1,
                    caseDistrictId: "510105",
                    fullName: "青羊区",
                    lat: 30.67387,
                    lng: 104.06151
                },
                {
                    CaseClosedNumber: 0,
                    CaseNotClosedNumber: 7,
                    caseCountAddNumber: 0,
                    caseCountNumber: 7,
                    caseDistrictId: "510129",
                    fullName: "大邑县",
                    lat: 30.58738,
                    lng: 103.52075
                },
                {
                    CaseClosedNumber: 0,
                    CaseNotClosedNumber: 1,
                    caseCountAddNumber: 0,
                    caseCountNumber: 1,
                    caseDistrictId: "510131",
                    fullName: "蒲江县",
                    lat: 30.19667,
                    lng: 103.50616
                },
                {
                    CaseClosedNumber: 2,
                    CaseNotClosedNumber: 1,
                    caseCountAddNumber: 0,
                    caseCountNumber: 3,
                    caseDistrictId: "510183",
                    fullName: "邛崃市",
                    lat: 30.41489,
                    lng: 103.46283
                },
                {
                    CaseClosedNumber: 2,
                    CaseNotClosedNumber: 0,
                    caseCountAddNumber: 0,
                    caseCountNumber: 2,
                    caseDistrictId: "510185",
                    fullName: "简阳市",
                    lat: 30.3904,
                    lng: 104.54864
                },
                {
                    CaseClosedNumber: 0,
                    CaseNotClosedNumber: 0,
                    caseCountAddNumber: 0,
                    caseCountNumber: 0,
                    caseDistrictId: "510106",
                    fullName: "金牛区",
                    lat: 30.69126,
                    lng: 104.05114
                },
                {
                    CaseClosedNumber: 0,
                    CaseNotClosedNumber: 0,
                    caseCountAddNumber: 0,
                    caseCountNumber: 0,
                    caseDistrictId: "510107",
                    fullName: "武侯区",
                    lat: 30.64235,
                    lng: 104.04303
                },
                {
                    CaseClosedNumber: 0,
                    CaseNotClosedNumber: 0,
                    caseCountAddNumber: 0,
                    caseCountNumber: 0,
                    caseDistrictId: "510112",
                    fullName: "龙泉驿区",
                    lat: 30.55658,
                    lng: 104.27462
                },
                {
                    CaseClosedNumber: 0,
                    CaseNotClosedNumber: 0,
                    caseCountAddNumber: 0,
                    caseCountNumber: 0,
                    caseDistrictId: "510113",
                    fullName: "青白江区",
                    lat: 30.87841,
                    lng: 104.251
                },
                {
                    CaseClosedNumber: 0,
                    CaseNotClosedNumber: 0,
                    caseCountAddNumber: 0,
                    caseCountNumber: 0,
                    caseDistrictId: "510114",
                    fullName: "新都区",
                    lat: 30.82314,
                    lng: 104.15921
                },
                {
                    CaseClosedNumber: 0,
                    CaseNotClosedNumber: 0,
                    caseCountAddNumber: 0,
                    caseCountNumber: 0,
                    caseDistrictId: "510115",
                    fullName: "温江区",
                    lat: 30.68444,
                    lng: 103.84881
                },
                {
                    CaseClosedNumber: 0,
                    CaseNotClosedNumber: 0,
                    caseCountAddNumber: 0,
                    caseCountNumber: 0,
                    caseDistrictId: "510116",
                    fullName: "双流区",
                    lat: 30.57444,
                    lng: 103.92373
                },
                {
                    CaseClosedNumber: 0,
                    CaseNotClosedNumber: 0,
                    caseCountAddNumber: 0,
                    caseCountNumber: 0,
                    caseDistrictId: "510117",
                    fullName: "郫都区",
                    lat: 30.81054,
                    lng: 103.88717
                },
                {
                    CaseClosedNumber: 0,
                    CaseNotClosedNumber: 0,
                    caseCountAddNumber: 0,
                    caseCountNumber: 0,
                    caseDistrictId: "510121",
                    fullName: "金堂县",
                    lat: 30.86195,
                    lng: 104.41195
                },
                {
                    CaseClosedNumber: 0,
                    CaseNotClosedNumber: 0,
                    caseCountAddNumber: 0,
                    caseCountNumber: 0,
                    caseDistrictId: "510132",
                    fullName: "新津县",
                    lat: 30.40983,
                    lng: 103.8114
                },
                {
                    CaseClosedNumber: 0,
                    CaseNotClosedNumber: 0,
                    caseCountAddNumber: 0,
                    caseCountNumber: 0,
                    caseDistrictId: "510182",
                    fullName: "彭州市",
                    lat: 30.99011,
                    lng: 103.958
                },
                {
                    CaseClosedNumber: 0,
                    CaseNotClosedNumber: 0,
                    caseCountAddNumber: 0,
                    caseCountNumber: 0,
                    caseDistrictId: "510184",
                    fullName: "崇州市",
                    lat: 30.63014,
                    lng: 103.67285
                },
                {
                    CaseClosedNumber: 0,
                    CaseNotClosedNumber: 0,
                    caseCountAddNumber: 0,
                    caseCountNumber: 0,
                    caseDistrictId: "510186",
                    fullName: "天府新区",
                    lat: 30.523771,
                    lng: 104.069469
                },
                {
                    CaseClosedNumber: 0,
                    CaseNotClosedNumber: 0,
                    caseCountAddNumber: 0,
                    caseCountNumber: 0,
                    caseDistrictId: "510187",
                    fullName: "高新南区",
                    lat: 30.595067,
                    lng: 104.067125
                },
                {
                    CaseClosedNumber: 0,
                    CaseNotClosedNumber: 0,
                    caseCountAddNumber: 0,
                    caseCountNumber: 0,
                    caseDistrictId: "510188",
                    fullName: "高新西区",
                    lat: 30.766486,
                    lng: 103.930357,
                },
                                {
                    CaseClosedNumber: 0,
                    CaseNotClosedNumber: 0,
                    caseCountAddNumber: 0,
                    caseCountNumber: 0,
                    caseDistrictId: "510189",
                    fullName: "高新东区",
                    lat: 30.766486,
                    lng: 103.930357,
                }]
            }
        }
    },
    methods: {
        // 旧数据
        // mapInit () {
        //     // 地图上的数据为假数据，所需的数据由自己处理放入就可使用
        //     let myChartDiv = this.$refs.mapDiv;
        //     if (myChartDiv) {
        //         let myChart = echarts.init(myChartDiv);
        //         echarts.registerMap('chengdu', geoJson);
        //         let option = {
        //             title: {
        //                 text: '成都市旧地图（有新成都geojson请发给我^_^!）',
        //                 x: 'center',
        //                 textStyle: {
        //                     color: '#000'
        //                 }
        //             },
        //             tooltip: { //提示框组件。
        //                 trigger: 'item', //数据项图形触发，主要在散点图，饼图等无类目轴的图表中使用。
        //                 formatter: function (data) {
        //                     let str = `<div><span style="width: 4px;height: 4px; background: #f2ae5d;display: inline-block;border: 3px solid #f2ae5d;border-radius: 50%;"></span>&nbsp;&nbsp;<span style="color: #aaa;">案发数：</span> ${data.data.num}</div> <br/>
        //                 <span style="width: 4px;height: 4px; background: #f2ae5d;display: inline-block;border: 3px solid #f2ae5d;border-radius: 50%;"></span>&nbsp;&nbsp;<span style="color: #aaa;">已侦破：</span> ${data.data.already}`
        //                     return str
        //                 },
        //                 backgroundColor: 'rgb(37 41 53 / 0.8)',
        //                 borderWidth: 1,
        //                 borderColor: 'rgb(37 41 53 / 0.8)',
        //                 padding: 10,
        //                 textStyle: {
        //                     fontSize: '24px',
        //                     color: '#fff',
        //                 },
        //                 extraCssText: 'width: 210px;height: 80px;',
        //                 borderRadius: 5
        //             },
        //             geo: {
        //                 show: true,
        //                 map: 'chengdu',
        //                 roam: false,
        //                 itemStyle: {
        //                     normal: {
        //                         areaColor: '#2d3443',
        //                         shadowColor: 'rgba(0,0,0,0.6)',
        //                         shadowOffsetX: 25,
        //                         shadowOffsetY: 25,
        //                         shadowBlur: 15
        //                     },
        //                 },
        //             },
        //             visualMap: //地图背景色根据数据自动变色
        //                 [{
        //                     x: 'left',
        //                     y: 'center',
        //                     seriesIndex: [0],
        //                     show: false,
        //                     min: 0,
        //                     max: 400,
        //                     text: ['High', 'Low'],
        //                     realtime: false,
        //                     calculable: false,
        //                     // color: ['#2d3443', '#4a5365'], //根据数据量地图变色，使用inRange会覆盖圆圈的颜色
        //                     textStyle: {
        //                         color: '#7986a1'
        //                     },
        //                     inRange: {
        //                         color: ['#2d3443', '#4a5365']
        //                     }
        //                 }],
        //             series: [
        //                 {
        //                     name: `地区：`,
        //                     type: 'map',
        //                     zoom: 1.1,
        //                     roam: false, //是否开启鼠标缩放和平移
        //                     label: {
        //                         normal: {
        //                             show: true,
        //                             textStyle: {
        //                                 color: '#7986a1'
        //                             }
        //                         },
        //                         emphasis: {
        //                             textStyle: {
        //                                 color: '#fff' //移入文字颜色
        //                             }
        //                         }
        //                     },
        //                     itemStyle: {
        //                         normal: {
        //                             borderColor: '#474b53', //边框颜色
        //                             borderWidth: 1,
        //                             areaColor: '#545c6f'
        //                         },
        //                         emphasis: { //是图形在高亮状态下的样式,比如在鼠标悬浮或者图例联动高亮时
        //                             areaColor: '#fabb49',
        //                             borderWidth: 0,
        //                             color: 'green'
        //                         }
        //                     },
        //                     map: 'chengdu',
        //                     data: mapPoint
        //                 },
        //                 {
        //                     type: 'effectScatter',
        //                     coordinateSystem: 'geo',
        //                     showEffectOn: 'render',
        //                     symbolSize: function (value, data) {
        //                         return data.data.num/100;  //计算圈大小
        //                     },
        //                     rippleEffect: {
        //                         period: 15,
        //                         scale: 4,
        //                         brushType: 'fill'
        //                     },
        //                     hoverAnimation: false,
        //                     itemStyle: {
        //                         normal: {
        //                             color: '#ffb965',
        //                             shadowBlur: 10,
        //                             shadowColor: '#333'
        //                         }
        //                     },
        //                     data: mapPoint
        //                 }
        //             ]
        //         };
        //         this.$nextTick(() => {
        //             myChart.setOption(option);
        //         })
        //     }
        // },

        //新的数据
        mapInit () {
            let myChartDiv = this.$refs.mapDiv;
            if (myChartDiv) {
                let myChart = echarts.init(myChartDiv);
                echarts.registerMap('chengdu', geoJson);
                let mapPointDa = this.caseBigData.caseDistrictStatisticsDtoList.map(item => { return { name: item.fullName, caseCountNumber: item.caseCountNumber, already: item.CaseClosedNumber, value: item.CaseNotClosedNumber } });
                // debugger
                //给图有数据的画圈，没数据的没有
                for (let i = 0; i < this.caseBigData.caseDistrictStatisticsDtoList.length; i++) {
                    for (let j = 0; j < mapPoint.length; j++) {
                        if (mapPoint[j].name == this.caseBigData.caseDistrictStatisticsDtoList[i].fullName) {
                            mapPoint[j].number = this.caseBigData.caseDistrictStatisticsDtoList[i].caseCountNumber;
                            mapPoint[j].caseCountNumber = this.caseBigData.caseDistrictStatisticsDtoList[i].caseCountNumber;
                            mapPoint[j].already = this.caseBigData.caseDistrictStatisticsDtoList[i].CaseClosedNumber;
                            mapPoint[j].caseCountAddNumber = this.caseBigData.caseDistrictStatisticsDtoList[i].caseCountAddNumber;
                        }
                    }
                }
                let option = {
                    title: {
                        x: 'center',
                        textStyle: {
                            color: '#000'
                        }
                    },
                    tooltip: { //提示框组件。
                        trigger: 'item', //数据项图形触发，主要在散点图，饼图等无类目轴的图表中使用。
                        formatter: function (data) {
                            let str = `<div><span style="width: 4px;height: 4px; background: #f2ae5d;display: inline-block;border: 3px solid #f2ae5d;border-radius: 50%;"></span>&nbsp;&nbsp;<span style="color: #aaa;">案发数：</span> ${data.data.caseCountNumber}</div> <br/>
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
                            max: 100,
                            text: ['High', 'Low'],
                            realtime: false,
                            calculable: false,
                            // color: ['#2d3443','#4a5365'], //根据数据量地图变色，使用inRange会覆盖圆圈的颜色
                            textStyle: {
                                color: '#7986a1'
                            },
                            inRange: {
                                color: ['#4a5365', '#242a36'],
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
                            data: mapPointDa
                        },
                    ]
                };
                this.$nextTick(() => {
                    myChart.setOption(option);
                    setTimeout(() => {
                        option.series[1] = {
                            type: 'effectScatter',
                            coordinateSystem: 'geo',
                            showEffectOn: 'render',
                            symbolSize: function (value, data) {
                                return data.data.caseCountAddNumber == 0 ? 0 : 10;  //计算圈大小
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
                        myChart.setOption(option);
                    }, 5000)
                })
            }
        },
    }
}
</script>