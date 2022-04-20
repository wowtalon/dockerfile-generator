<template>
    <el-card>
        <template #header>
            <div class="card-header">
                <span>基础配置</span>
            </div>
        </template>
        <div class="config-wrapper">
            <p>Docker 版本</p>
            <el-select v-model="version">
                <el-option
                v-for="item in options"
                :key="item.value"
                :label="item.lable"
                :value="item.value" />
            </el-select>
        </div>
        <div class="config-wrapper">
            <p>多阶段构建</p>
            <el-checkbox v-model="multiStage">开启</el-checkbox>
        </div>
        <div class="config-wrapper">
            <p>基础镜像</p>
            <el-input placeholder="基础镜像"></el-input>
        </div>
    </el-card>
</template>

<script>
const options = [
    {
        value: '1.12及以上',
        label: '1.12'
    },
    {
        value: '1.12以下',
        label: '1.0'
    }
]

export default {
    data() {
        return {
            options: options,
            version: '',
            multiStage: false
        }
    }
}
</script>

<style scoped>
.config-wrapper {
    display: inline-block;
}

.config-wrapper:not(:first-child) {
    margin-left: 20px;
}
</style>