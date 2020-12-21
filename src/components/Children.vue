/* eslint-disable vue/return-in-computed-property */
<template>
  <div class="parent">
    <h1>{{ msg }}</h1>
    <h2>title: {{ title }}</h2>
    <h2>date: {{ date }}</h2>
  </div>
</template>

<script>
export default {
  name: 'Parent',
  data () {
    return {
      msg: '你好我是子组件'
    }
  },
  props: {
    title: {
      type: String,
      default: '默认标题'
    },
    date: {
      type: String,
      default: ''
    }
  }
}
</script>

<style scoped>
h1 {
  font-weight: normal;
}

</style>
