<template>
    <d2-container>
        注意底部水印^_^!
    </d2-container>
</template>

<script>
export default {
    name: 'markWater',
    data () {
        return {

        }
    },
    mounted () {
        this.setWatermark('tix')
    },
    methods: {
        setWatermark (str) {
            let id = '1.23452384164.123412415'

            if (document.getElementById(id) !== null) {
                document.body.removeChild(document.getElementById(id))
            }

            let can = document.createElement('canvas')
            can.width = 200
            can.height = 120

            let cans = can.getContext('2d')
            cans.rotate(-20 * Math.PI / 180)
            cans.font = 'bold 46px Microsoft YaHei '
            cans.fillStyle = 'rgba(42,46,56, 0.02)'
            cans.textAlign = 'left'
            cans.textBaseline = 'Middle'
            cans.fillText(str, 0, can.height)

            let div = document.createElement('div')
            div.id = id
            div.style.pointerEvents = 'none'
            div.style.top = '60px'
            div.style.left = '0px'
            div.style.position = 'fixed'
            div.style.zIndex = '100000'
            div.style.width = document.documentElement.clientWidth + 'px'
            div.style.height = document.documentElement.clientHeight + 'px'
            div.style.background = 'url(' + can.toDataURL('image/png') + ') left top repeat'
            document.body.appendChild(div)
            return id
        }
    }
}
</script>

