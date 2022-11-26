<template>
<div>
        <form @submit.prevent>
  <h4>Создание поста</h4>
  <input v-model="post.title" class="input" type="text" placeholder="Название">
  <input  v-model="post.body" class="input" type="text" placeholder="Создание">
  <button @click="createPost" class="btn">Создать</button>
</form>


<ul>
  <li v-for="c in x" :key="c.author.login">
  {{ c.author.login }}</li>
</ul>

</div>
  </template>
  
  <script>
  export default {
      props: ['x'],
      data() {
          return {
              post: {
                  title: '',
                  body: ''
              }
          }
      },

      methods: {
        createPost() {
      this.post.id = Date.now(),
      this.$emit('create', this.post),
      this.post = {
          title: '',
          body: ''
      }
  }
}
  }
  </script>
  
  <style>
  .btn {
  margin-top: 15px;
  align-self: flex-end;
  width: 100px;
  height: 40px;
  padding: 10px 15px;
  background: none;
  color: teal;
  /* border: 2px solid teal; */
}

form {
  display: flex;
  flex-direction: column;
}
  </style>