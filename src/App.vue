<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" name="atom" age="12" adress="sfsdfsdfsdfsdfsdf" />
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      arr: [
        { label: 'label', value: 'value' },
        { label: 'label', value: 'value' },
        { label: 'label', value: 'value' },
        { label: 'label', value: 'value' },
        { label: 'label', value: 'value' },
        { label: 'label', value: 'value' },
        { label: 'label', value: 'value' }
      ]
    }
  },
  methods: {
    getInfo() {
      return this.arr.map(item => (item.value = item.label += item.value))
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
