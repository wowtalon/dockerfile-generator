<template>
  <h1>Dockerfile 生成</h1>
  <docker-config></docker-config>
  <stage-config></stage-config>
  <h2>源代码</h2>
  <p><el-link type="primary" href="https://github.com/wowtalon/dockerfile-generator">github</el-link></p>
</template>

<script>
import DockerConfig from './components/DockerConfig.vue'
import StageConfig from './components/StageConfig.vue'

export default {
  name: 'App',
  components: {
    DockerConfig,
    StageConfig
  }
}
</script>


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  width: 980px;
  margin: 0 auto;
  margin-top: 40px;
}

</style>
