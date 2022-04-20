<template>
    <el-card>
        <template #header>
            <div class="card-header">
                <span>构建步骤</span>
            </div>
        </template>
        <div class="stage-wrapper">
            <el-collapse>
                <el-collapse-item v-for="action in actions" :title="action.name" :key="action.name">
                    <p>{{ action.inst }}</p>
                </el-collapse-item>
            </el-collapse>
        </div>
        <div class="new-action-wrapper">
            <el-select v-model="new_action">
                <el-option
                v-for="(value, key) in action_type"
                :key="key"
                :label="value"
                :value="key" />
            </el-select>
            <div class="new_action_config">
                <el-input v-model="new_action_key" placeholder="输入键名"></el-input>
                <el-input v-model="new_action_value" placeholder="输入值"></el-input>
            </div>
            <el-button type="primary" @click="add_action">添加步骤</el-button>
        </div>
    </el-card>
</template>

<script>

const action_type = {
    "ARG": "声明键值/ARG",
    "RUN": "执行命令/RUN",
    "LABEL": "元数据/LABEL",
    "EXPOSE": "发布端口/EXPOSE",
    "ENV": "环境变量/ENV",
    "ADD": "添加文件/ADD",
    "COPY": "添加文件/COPY",
    "WORKDIR": "修改工作路径/WORKDIR",
    "CMD": "CMD"
}

export default {
    data() {
        return {
            actions: [
                {
                    name: "初始化容器",
                    inst: "FROM ubuntu:latest"
                }
            ],
            new_action: '',
            action_type: action_type,
            new_action_key: '',
            new_action_value: ''
        }
    },
    methods: {
        add_action() {
            let that = this
            that.actions.push({
                name: action_type[that.new_action],
                inst: `${that.new_action} ${that.new_action_key} ${that.new_action_value}`
            })
            that.new_action = ""
            that.new_action_key = ""
            that.new_action_value = ""
        }
    }
}
</script>

<style scoped>
.el-card {
    margin-top: 40px;
}

.config-wrapper, .new_action_config {
    display: inline-block;
}

.new_action_config {
    margin: 20px 0;
    display: flex;
    flex-direction: row;
}

.new_action_config>.el-input {
    width: 40%;
}

.new_action_config>.el-input:not(:first-child) {
    margin-left: 20px;
}

.config-wrapper:not(:first-child) {
    margin-left: 20px;
}

.new-action-wrapper {
    margin-top: 20px;
}
</style>