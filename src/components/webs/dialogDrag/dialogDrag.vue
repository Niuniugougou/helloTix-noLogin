<template>
    <div>
        <div>
            可拖拽弹框。
        </div>
        <el-dialog v-dialogDrag
                   title="拖拽"
                   :visible.sync="dialogVisible"
                   v-if="dialogVisible"
                   width="460px"
                   height="200px"
                   :show-close="false"
                   :close-on-press-escape="false"
                   :close-on-click-modal="true">
            <div>
                拖拽。
            </div>
        </el-dialog>
    </div>
</template>
<script>
export default {
    data() {
        return {
            dialogVisible: true
        }
    }
}
</script>