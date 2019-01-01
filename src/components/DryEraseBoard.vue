<template>
  <div class="hello">
    <input type="text" name="" value="" placeholder="Title" v-model="title">
    <br>
    <textarea name="name" rows="8" cols="80" v-model="content"></textarea>
    <br>
    <button class="btn" type="button" name="button" @click="post">Send it!</button>
    <br>
    <div
      class="post"
      v-for="post in posts"
      :key="post.title">
        <code>
          {{ post.title }}
          <br>
          {{ post.content }}
        </code>
    </div>
  </div>
</template>

<script>
import { namesRef } from '../firebase';
export default {
  name: 'DryEraseBoard',
  data() {
    return {
      title: '',
      content: '',
      posts: {}
    }
  },
  methods: {
    post() {
      namesRef.child(this.title).set({
        title: this.title,
        content: this.content
      })
      this.title = '';
      this.content = '';
    }
  },
  created() {
    namesRef.on('value', (snapshot) => {
      console.log('the snapshot', JSON.stringify(snapshot.val(), null, 2))
      this.posts = snapshot.val();
    })
  }
}
</script>
