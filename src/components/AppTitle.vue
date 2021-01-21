<template>
  <div>
    <h1>{{ title }}</h1>
  </div>
</template>
<script>
export default {
  // props: ['title']
  props: {
    title: {
      type: String,
      require: true
    }
  }
}
</script>