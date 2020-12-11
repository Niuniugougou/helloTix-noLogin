<template>
    <div>
        <div>G6Demo1</div>
        <div id="G6Demo1"></div>
    </div>
</template>
<script>
import G6 from '@antv/g6';
// import insertCss from 'insert-css';
// insertCss(`
//   .g6-tooltip {
//     border-radius: 6px;
//     font-size: 12px;
//     color: #fff;
//     background-color: #000;
//     padding: 2px 8px;
//     text-align: center;
//   }
// `);
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
            //此自定义节点未生效
            G6.registerNode(
                'justPoints',
                {
                    drawShape (cfg, group) {
                        const rect = group.addShape('rect', {
                            attrs: {
                                x: -75,
                                y: -25,
                                width: 150,
                                height: 50,
                                radius: 10,
                                stroke: '#5B8FF9',
                                fill: '#C6E5FF',
                                lineWidth: 3,
                            },
                            name: 'rect-shape',
                        });
                        if (cfg.name) {
                            group.addShape('text', {
                                attrs: {
                                    text: cfg.name,
                                    x: 0,
                                    y: 0,
                                    fill: '#00287E',
                                    fontSize: 14,
                                    textAlign: 'center',
                                    textBaseline: 'middle',
                                    fontWeight: 'bold',
                                },
                                name: 'text-shape',
                            });
                        }
                        return rect;
                    },
                },
                'single-node',
            );
            this.$nextTick(() => {
                let data = {
                    nodes: [
                        {
                            id: '1',
                            type: 'justPoints',
                            label: '张三',
                            name: '666666666'
                        },
                        {
                            id: '2',
                            type: 'justPoints',
                            label: '李四'
                        },
                        {
                            id: '3',
                            type: 'justPoints',
                            label: '王五'
                        },
                        {
                            id: '4',
                            type: 'justPoints',
                            label: '赵六'
                        }
                    ],
                    edges: [
                        {
                            source: '1',
                            target: '2',
                            label: 'hhhhhh'
                        },
                        {
                            source: '1',
                            target: '3',
                            label: 'ggggggg'
                        },
                        {
                            source: '2',
                            target: '4',
                            label: 'jjjjjjj'
                        },
                        {
                            source: '3',
                            target: '4',
                            label: 'kkkkkk'
                        }
                    ],
                };
                const container = document.getElementById('G6Demo1');
                const width = container.scrollWidth || 500;
                const height = container.scrollHeight || 500;
                this.treeOne = new G6.Graph({
                    container: 'G6Demo1',
                    width,
                    height,
                    layout: {
                        type: 'dagre',
                        nodesepFunc: (d) => {
                            if (d.id === '3') {
                                return 500;
                            }
                            return 50;
                        },
                        ranksep: 70,
                        controlPoints: true,
                    },
                    defaultNode: {
                        type: 'justPoints',
                        anchorPoints: [
                            [0, 0.5],
                            [1, 0.5],
                        ],
                    },
                    defaultEdge: {
                        type: 'polyline',
                        style: {
                            radius: 20,
                            offset: 45,
                            endArrow: true,
                            lineWidth: 2,
                            stroke: '#C2C8D5',
                        },
                        style: {
                            stroke: '#b5b5b5',
                            lineAppendWidth: 3, // Enlarge the range the edge to be hitted
                        },
                        labelCfg: {
                            autoRotate: true,
                            style: {
                                // A white stroke with width 5 helps show the label more clearly avoiding the interference of the overlapped edge
                                stroke: 'white',
                                lineWidth: 5,
                            },
                        },
                    },
                    nodeStateStyles: {
                        selected: {
                            stroke: '#d9d9d9',
                            fill: '#5394ef',
                        },
                    },
                    modes: {
                        default: [
                            'drag-canvas',
                            'zoom-canvas',
                            'click-select',
                            // {
                            //     type: 'tooltip',
                            //     formatText (model) {
                            //         const cfg = model.conf;
                            //         const text = [];
                            //         cfg.forEach((row) => {
                            //             text.push(row.label + ':' + row.value + '<br>');
                            //         });
                            //         return text.join('\n');
                            //     },
                            //     offset: 30,
                            // },
                        ],
                    },
                    fitView: true,
                });
                this.treeOne.data(data);
                this.treeOne.render();
            })
        }
    }
}
</script>