<template>
  <div class="container">
    <p>
      <button class="btn primary" @click="$emit('load')">
        Загрузить комментарии
      </button>
    </p>
    <div class="card" v-if="comments.length !== 0">
      <h2>Комментарии</h2>
      <ul class="list">
        <li class="list-item" v-for="comment in comments" :key="comment.id">
          <div>
            <h3>{{ comment.name }}</h3>
            <p>
              <strong>{{ comment.email }}</strong>
            </p>
            <small>{{ comment.body }}</small>
          </div>
        </li>
      </ul>
    </div>
    <div class="card center" v-else>
      <h4>Нет коментриеев</h4>
    </div>
  </div>
</template>

<script>
export default {
  emits: ['load'],
  props: ['comments']
}
</script>