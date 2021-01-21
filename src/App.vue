
<template>
  <div class="container column">
    <!-- ========= Comp FORM Left Block-->
    <app-add-contents @submit.prevent="send">
      <template #type>
        <div class="form-control">
          <label for="type">Тип блока</label>
          <select id="type" v-model="selectDefault">
            <option
              v-for="(options, key) in selectOptions"
              :value="options.value"
              :key="key"
            >
              {{ options.text }}
            </option>
          </select>
        </div>
      </template>
      <!-- ====================== -->
      <template #values>
        <div class="form-control">
          <label for="value">Значение</label>
          <textarea id="value" rows="3" v-model.trim="content"></textarea>
          <!-- content -->
        </div>
      </template>
      <!-- ================ BUTTON -->
      <template #btn>
        <button
          type="button"
          class="btn primary"
          @click="send"
          :disabled="_isActiveButton"
        >
          Добавить
        </button></template
      >
    </app-add-contents>
    <!-- ========= Comp Right Block-->
    <app-block :obtainedValues="obtainedValues"></app-block>
  </div>
  <!-- ========= Comp Loading and DataBase-->
  <app-loader v-if="loading"></app-loader>
  <app-comments-data-base
    v-else
    :comments="comments"
    @load="loadComments"
  ></app-comments-data-base>
</template>

<script>
import AppAddContents from '@/components/AppAddContents'
import AppBlock from '@/components/AppBlock'
import AppCommentsDataBase from '@/components/AppCommentsDataBase'
import AppLoader from '@/components/AppLoader'

export default {
  data() {
    return {
      selectDefault: 'title',
      selectOptions: [
        { value: 'title', text: 'Заголовок' },
        { value: 'subtitle', text: 'Подзаголовок' },
        { value: 'avatar', text: 'Аватар' },
        { value: 'text', text: 'Текст' }
      ],
      content: '',
      obtainedValues: [],
      comments: [],
      loading: false
    }
  },
  methods: {
    send() {
      // отправка в  обькт (obtainedValues)
      this.obtainedValues.push({
        value: this.selectDefault,
        text: this.content
      })
      this.selectDefault = 'title'
      this.content = ''
    },
    async loadComments() {
      try {
        this.loading = true
        const request = await fetch(
          'https://jsonplaceholder.typicode.com/comments?_limit=42'
        )
        if (!request) {
          throw new Error('The list of comments is empty')
        }
        this.comments = await request.json()
        this.loading = false
      } catch (error) {
        console.warn('Errors')
      }
    }
  },
  computed: {
    // состояние кнопки
    _isActiveButton() {
      return this.content.length < 4
    }
  },
  components: {
    AppAddContents,
    AppBlock,
    AppCommentsDataBase,
    AppLoader
  }
}
</script>

<style lang="scss">
.avatar {
  display: flex;
  justify-content: center;
}

.avatar img {
  width: 150px;
  height: auto;
  border-radius: 50%;
}
</style>
