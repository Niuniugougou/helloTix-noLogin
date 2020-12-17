/*
 * @Author: tix 
 * @Date: 2020-12-17 11:03:18 
 * @Last Modified by: akang
 * @Last Modified time: 2020-12-17 11:43:37
 */
/*
 * @type: primary / success / info / warning / danger
 * @icon: icon 的类名 
 * @isCircle: 是否是圆形
 */


<template>
    <el-button @click="downloadimg"
               :type="type"
               :icon="icon"
               :circle="cisCircle">{{cbuttonName}}</el-button>
</template>
<script>
import G6 from '@antv/g6';

export default {
    props: {
        chartRef: Object,
        downloadName: String,
        buttonName: String,
        iconName: String,
        typeName: String,
        isCircle: Boolean,
    },
    data () {
        return {
            treeOne: this.chartRef,
            cdownloadName: this.downloadName != '' ? this.downloadName : 1,
            cbuttonName: this.buttonName != '' ? this.buttonName : '',
            icon: this.iconName ? this.iconName : null,
            type: this.typeName ? this.typeName : null,
            cisCircle: this.isCircle
        }
    },
    watch: {
        chartRef: {
            handler: function (val, oldval) {
                if (val != oldval) {
                    this.treeOne = val
                }
            },
            immediate: true,
            deep: true
        },
    },
    methods: {
        downloadimg () {
            let url = this.treeOne.toDataURL('image/png', '#fff');
            let a = document.createElement("a");
            a.download = this.cdownloadName;
            a.href = url;
            a.setAttribute("id", "donwLoadImg");
            // 防止反复添加
            if (document.getElementById("donwLoadImg")) {
                document.body.removeChild(
                    document.getElementById("donwLoadImg")
                );
            }
            document.body.appendChild(a);
            a.click();
        }
    }
}
</script>