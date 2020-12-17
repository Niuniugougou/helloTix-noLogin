<template>
    <d2-container>
        <div style="position:absolute;">
            G6Demo1--自定义图形、拖拽、移入效果（建议G6版本大于3.8.3）
            <el-button @click="downloadimg">导出图片</el-button>
        </div>
        <div id="G6Demo1" style="height: 100%;"></div>
    </d2-container>
</template>
<script>
import G6 from '@antv/g6';
export default {
    data () {
        return {
            treeOne: null,
        }
    },
    mounted () {
        this.drawTree();
    },
    methods: {
        drawTree () {
            if (this.treeOne) {
                this.treeOne.destroy();
                this.treeOne = null;
            }
            const data = {
                nodes: [
                    {
                        id: 'node1',
                        // x: 500,
                        // y: 100,
                        type: 'circle-shape-animate',
                        size: 20,
                        color: '#40a9ff',
                        label: '嘿'
                    },
                    {
                        id: 'node2',
                        // x: 100,
                        // y: 200,
                        type: 'rect-shape',
                        color: '#40a9ff',
                        label: '李四2'
                    },
                    {
                        id: 'node3',
                        // x: 300,
                        // y: 200,
                        type: 'rect-shape',
                        label: '王五3'
                    },
                    {
                        id: 'node4',
                        // x: 500,
                        // y: 200,
                        type: 'rect-shape',
                        label: '赵六4'
                    },
                    {
                        id: 'node5',
                        // x: 700,
                        // y: 200,
                        type: 'rect-shape',
                        label: '朱天诺5'
                    },
                    {
                        id: 'node6',
                        // x: 100,
                        // y: 300,
                        type: 'rect-shape',
                        label: '张杰6'
                    },
                    {
                        id: 'node7',
                        // x: 300,
                        // y: 300,
                        type: 'rect-shape',
                        label: '张已7'
                    },
                    {
                        id: 'node8',
                        // x: 500,
                        // y: 300,
                        type: 'rect-shape',
                        label: '张丙8'
                    },
                    {
                        id: 'node9',
                        // x: 500,
                        // y: 400,
                        type: 'circle-shape',
                        label: '团体9'
                    },
                ],
                edges: [
                    {
                        source: 'node1',
                        target: 'node2',
                        label: '交易、碰面'
                    },
                    {
                        source: 'node1',
                        target: 'node3',
                        label: '联系'
                    },
                    {
                        source: 'node1',
                        target: 'node4',
                        label: '交易'
                    },
                    {
                        source: 'node2',
                        target: 'node3',
                        label: '交易'
                    },
                    {
                        source: 'node1',
                        target: 'node5',
                        label: '交易、碰面'
                    },
                    {
                        source: 'node2',
                        target: 'node6',
                        label: '碰面'
                    },
                    {
                        source: 'node2',
                        target: 'node7',
                        label: '交易、碰面'
                    },
                    {
                        source: 'node6',
                        target: 'node9',
                        label: '交易、碰面'
                    },
                    {
                        source: 'node8',
                        target: 'node9',
                        label: '碰面'
                    },
                    {
                        source: 'node5',
                        target: 'node9',
                        label: '碰面'
                    },
                    {
                        source: 'node7',
                        target: 'node9',
                        label: '碰面'
                    },
                ],
            };

            G6.registerNode(
                'rect-shape',
                {},
                'rect',
            );

            G6.registerNode(
                'circle-shape',
                {},
                'circle',
            );

            G6.registerNode(
                'circle-shape-animate',
                {
                    afterDraw (cfg, group) {
                        const r = cfg.size ? cfg.size / 2 : 20;
                        const back1 = group.addShape('circle', {
                            zIndex: -3,
                            attrs: {
                                x: 0,
                                y: 0,
                                r,
                                fill: cfg.color,
                                opacity: 0.6,
                            },
                            name: 'back1-shape',
                        });
                        const back2 = group.addShape('circle', {
                            zIndex: -2,
                            attrs: {
                                x: 0,
                                y: 0,
                                r,
                                fill: cfg.color,
                                opacity: 0.6,
                            },
                            name: 'back2-shape',
                        });
                        const back3 = group.addShape('circle', {
                            zIndex: -1,
                            attrs: {
                                x: 0,
                                y: 0,
                                r,
                                fill: cfg.color,
                                opacity: 0.6,
                            },
                            name: 'back3-shape',
                        });
                        group.sort(); // Sort according to the zIndex
                        back1.animate(
                            {
                                r: r + 10,
                                opacity: 0.1,
                            },
                            {
                                duration: 3000,
                                easing: 'easeCubic',
                                delay: 0,
                                repeat: true, // repeat
                            },
                        ); // no delay
                        back2.animate(
                            {
                                r: r + 10,
                                opacity: 0.1,
                            },
                            {
                                duration: 3000,
                                easing: 'easeCubic',
                                delay: 1000,
                                repeat: true, // repeat
                            },
                        ); // 1s delay
                        back3.animate(
                            {
                                r: r + 10,
                                opacity: 0.1,
                            },
                            {
                                duration: 3000,
                                easing: 'easeCubic',
                                delay: 2000,
                                repeat: true, // repeat
                            },
                        ); // 3s delay
                    },
                },
                'circle', //以什么内置类型为基础扩展，可以不写
            );

            const container = document.getElementById('G6Demo1');
            const width = container.scrollWidth;
            const height = container.scrollHeight || 500;
            this.treeOne = new G6.Graph({
                container: 'G6Demo1',
                width,
                height,
                fitCenter: true,
                defaultNode: {
                    type: 'rect',
                    size: [80, 40],
                    style: {
                        fill: '#fff',
                        stroke: '#5B8FF9',
                    },
                },
                defaultEdge: {
                    style: {
                        lineWidth: 1,
                        stroke: '#b5b5b5',
                    },
                    // type: 'cubic-horizontal' //贝塞尔曲线
                    // type: 'cubic-vertical',  //三次贝塞尔曲线
                },
                modes: {
                    default: [
                        'drag-canvas', //拖动画布
                        'zoom-canvas', //鼠标滚轮
                        'click-select', //鼠标点击
                        'drag-node', //拖动节点
                        'activate-relations', //移入显示相连节点
                    ],
                },
                layout: {
                    type: 'dagre', //层次布局
                    rankdir: 'TB', // 可选，默认为图的中心
                    align: 'DL', // 可选
                    nodesep: 50, // 可选，默认为50
                    ranksep: 50, // 可选，默认为50
                    controlPoints: true, // 可选，是否保留布局连线的控制点
                    sortByCombo: true, //同一层节点是否根据每个节点数据中的 comboId 进行排序，以防止 combo 重叠
                },
            });
            this.treeOne.read(data);
        },
        downloadimg () {
            let url = this.treeOne.toDataURL('image/png','#fff');
            let a = document.createElement("a");
            a.download = 1;
            a.href = url;
            a.setAttribute("id", "donwLoadData");
            // 防止反复添加
            if (document.getElementById("donwLoadData")) {
                document.body.removeChild(
                    document.getElementById("donwLoadData")
                );
            }
            document.body.appendChild(a);
            a.click();
        }
    }
}
</script>