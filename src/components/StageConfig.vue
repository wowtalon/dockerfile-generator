<template>
  <el-card>
    <template #header>
      <div class="card-header">
        <span>构建步骤</span>
      </div>
    </template>
    <div class="stage-wrapper">
      <el-collapse>
        <el-collapse-item
          v-for="(action, index) in actions"
          :title="action.name"
          :key="action.name"
        >
          <p>{{ action.inst }}</p>
          <el-button type="danger" @click="delete_action(index)">删除</el-button>
        </el-collapse-item>
      </el-collapse>
    </div>
    <div class="new-action-wrapper">
      <el-select v-model="new_action" @change="select_action">
        <el-option
          v-for="(value, key) in action_type"
          :key="key"
          :label="value"
          :value="key"
        />
      </el-select>
      <div class="new_action_config">
        <el-input
          v-model="new_action_key"
          :placeholder="key_placeholder"
        ></el-input>
        <el-input
          v-if="has_key"
          v-model="new_action_value"
          :placeholder="value_placeholder"
        ></el-input>
      </div>
      <el-button type="primary" @click="add_action">添加步骤</el-button>
    </div>
  </el-card>
  <el-card>
    <template #header>
      <div class="card-header">
        <span>Dockerfile 预览</span>
      </div>
    </template>
    <el-input
      v-model="dockerfile"
      autosize
      type="textarea"
    />
  </el-card>
</template>

<script>
const action_type = {
  ARG: "声明键值/ARG",
  RUN: "执行命令/RUN",
  LABEL: "元数据/LABEL",
  EXPOSE: "发布端口/EXPOSE",
  ENV: "环境变量/ENV",
  ADD: "添加文件/ADD",
  COPY: "添加文件/COPY",
  WORKDIR: "修改工作路径/WORKDIR",
  CMD: "CMD",
};

const placeholders = {
  ARG: ["输入键名", "输入值"],
  LABEL: ["输入键名", "输入值"],
  ENV: ["输入键名", "输入值"],
  ADD: ["输入源文件路径", "输入目的路径"],
  COPY: ["输入源文件路径", "输入目的路径"],
  RUN: ["输入命令"],
  EXPOSE: ["输入需要发布的端口"],
  WORKDIR: ["输入路径"],
  CMD: ["输入命令"],
};

export default {
  data() {
    return {
      actions: [
        {
          name: "初始化容器",
          inst: "FROM ubuntu:latest",
        },
      ],
      new_action: "",
      action_type: action_type,
      new_action_key: "",
      new_action_value: "",
      has_key: false,

      key_placeholder: "",
      value_placeholder: "",

      dockerfile: ""
    };
  },
  methods: {
    add_action() {
      let that = this;
      that.actions.push({
        name: action_type[that.new_action],
        inst: `${that.new_action} ${that.new_action_key} ${that.new_action_value}`,
      });
      that.new_action = ""
      that.new_action_key = ""
      that.new_action_value = ""

      that.update_dockerfile()
    },
    select_action(action) {
      console.log(action);
      this.key_placeholder = placeholders[action][0];
      if (placeholders[action].length > 1) {
        this.value_placeholder = placeholders[action][1];
        this.has_key = true;
      } else {
        this.has_key = false;
      }
    },
    delete_action(index) {
        this.actions.splice(index, 1)
        this.update_dockerfile()
        console.log(index)
    },
    update_dockerfile() {
        this.dockerfile = this.actions.map(el => { return el.inst }).join("\n")
    }
  },
};
</script>

<style scoped>
.el-card {
  margin-top: 40px;
}

.config-wrapper,
.new_action_config {
  display: inline-block;
}

.new_action_config {
  margin: 20px 0;
  display: flex;
  flex-direction: row;
}

.new_action_config > .el-input {
  width: 40%;
}

.new_action_config > .el-input:not(:first-child) {
  margin-left: 20px;
}

.config-wrapper:not(:first-child) {
  margin-left: 20px;
}

.new-action-wrapper {
  margin-top: 20px;
}
</style>