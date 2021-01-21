<template>
  <div>
    <h2>{{ subtitle }}</h2>
  </div>
</template>

<script>
export default {
  props: {
    subtitle: {
      type: String,
      require: true
    }
  }
}
</script>