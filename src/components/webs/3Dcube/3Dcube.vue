<template>
    <div class="wrap">
        <div class="cube">
            <div class="front">front</div>
            <div class="back">back</div>
            <div class="top">top</div>
            <div class="bottom">bottom</div>
            <div class="left">left</div>
            <div class="right">right</div>
        </div>
    </div>
</template>
<script>

</script>
<style scoped>
.wrap {
    width: 500px;
    height: 500px;
    perspective: 800px;
    /* 旋转原点 */
    perspective-origin: 50% 100px;
    margin-top: 300px;
    margin-left: 300px;
}
.cube {
    position: relative;
    width: 200px;
    height: 200px;
    /* 确保6个面都处于3D立体状态 */
    transform-style: preserve-3d;
    animation: spin 6s linear infinite;
    /*设置动画*/
}
.cube div {
    position: absolute;
    width: 200px;
    height: 200px;
    text-align: center;
    line-height: 200px;
    color: rgba(0, 0, 0, 0.5);
    font-family: sans-serif;
    text-transform: uppercase;
    background: rgba(255, 255, 255, 0.1);
    box-shadow: inset 0 0 30px rgba(125, 125, 125, 0.8);
}
/* 上下左右 */
@keyframes spin {
    /* from { transform: rotateY(0); }
    to { transform: rotateY(360deg); } */
    0% {
        transform: rotateX(0deg);
    }
    25% {
        transform: rotateX(180deg);
    }
    50% {
        transform: rotateX(360deg) rotateY(0deg);
    }
    75% {
        transform: rotateX(360deg) rotateY(180deg);
    }
    100% {
        transform: rotateX(360deg) rotateY(360deg);
    }
}
.back {
    transform: translateZ(-100px) rotateY(180deg);
}
.right {
    transform: rotateY(-270deg) translateX(100px);
    transform-origin: top right;
}
.front {
    transform: translateZ(100px);
}
.left {
    transform: rotateY(270deg) translateX(-100px);
    transform-origin: center left;
}
.top {
    transform: rotateX(-90deg) translateY(-100px);
    transform-origin: top center;
}
.bottom {
    transform: rotateX(90deg) translateY(100px);
    transform-origin: bottom center;
}
</style>