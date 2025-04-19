<template>
  <div id="app">
    <header>
      <h1>Vue 表单提交示例</h1>
    </header>
    <main>
      <FormComponent />
    </main>
  </div>
</template>

<script setup>
import FormComponent from './components/FormComponent.vue'
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin: 0;
  padding: 20px;
}

header {
  text-align: center;
  margin-bottom: 30px;
}

main {
  display: flex;
  justify-content: center;
}
</style>