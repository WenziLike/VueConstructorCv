<template>
  <div class="card card-w70" v-if="_presenceBlock">
    <div v-for="(item, key) in obtainedValues" :key="key">
      <!-- ========= Comp Title-->
      <app-title v-if="item.value === 'title'" :title="item.text"></app-title>
      <!-- ========= Comp Avatar-->
      <app-img v-else-if="item.value === 'avatar'" :url="item.text"></app-img>
      <!-- ========= Comp SubTitle-->
      <app-sub-title
        v-else-if="item.value === 'subtitle'"
        :subtitle="item.text"
      ></app-sub-title>
      <!-- ========= Comp Text-->
      <app-text v-else :text="item.text"></app-text>
    </div>
  </div>
  <div class="card card-w70" v-else>
    <h3>Добавьте первый блок, чтобы увидеть результат</h3>
  </div>
</template>

<script>
import AppTitle from '@/components/AppTitle'
import AppImg from '@/components/AppImg'
import AppSubTitle from '@/components/AppSubTitle'
import AppText from '@/components/AppText'

export default {
  props: {
    obtainedValues: {
      type: Array,
      require: true
    }
  },
  computed: {
    _presenceBlock() {
      return this.obtainedValues.length !== 0
    }
  },
  components: {
    AppTitle,
    AppImg,
    AppSubTitle,
    AppText
  }
}
</script>