<template>
  <div>
    これはコンポーネントから表示されています。
    <p>{{ message }}</p>
    <button @click="onClick">親メソッド実行</button>
  </div>
</template>

<script>
export default {
  props: ['message', 'isEnabled'],
  methods: {
    onClick () {
      this.$emit("toggle")
    }
  }
}
</script>

