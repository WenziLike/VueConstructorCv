<template>
  <div class="avatar">
    <img :src="url" />
  </div>
</template>

<script>
export default {
  props: {
    url: {
      type: String,
      require: true
    }
  }
}
</script>