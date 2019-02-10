<template>
  <div class="hello">
    <div class="form-group">
      <label class="form-label" for="input-example-1">Title</label>
      <input class="form-input" type="text" id="input-example-1" placeholder="Name" v-model="title">
    </div>
    <br>
    <div class="form-group">
      <label class="form-label" for="input-example-3">Content</label>
      <textarea class="form-input" id="input-example-3" placeholder="" rows="8" v-model="content"></textarea>
    </div>
    <br>
    <div class="form-group">
      <label for="input-example-2" class="form-label">Tags</label>
      <input type="text" id="input-example-2" class="form-input" v-model="tagsInput">
    </div>
    <br>
    <button class="btn btn-primary" type="button" name="button" @click="post">Post</button>
    <br>
    <DryErasePost
      v-for="(post, i) in posts"
      :id="`post-${i}`"
      :post="post"
      @deletePost="deletePost"/>
  </div>
</template>

<script>
import { namesRef } from '../firebase';
import DryErasePost from './DryErasePost';
export default {
  name: 'DryEraseBoard',
  components: {
    DryErasePost
  },
  data() {
    return {
      title: '',
      content: '',
      postId: 0,
      posts: {},
      tagsInput: ''
    }
  },
  methods: {
    clearFields() {
      this.title = '';
      this.content = '';
    },
    reset() {
      this.title = '';
      this.content = '';
      this.tagsInput = '';
    },
    post() {
      namesRef.child(`post-${this.postId}`).set({
        title: this.title,
        content: this.content,
        date: this.$moment().format('ll'),
        tags: this.tags
      });
      this.reset();
    },
    deletePost(id) {
      namesRef.child(id).remove()
    }
  },
  computed: {
    tags() {
      if(this.tagsInput != '') {
        let tags = this.tagsInput.split(',');
        tags = tags.map(tag => tag.trim())
        return tags;
      }else{
        return null;
      }
    },
  },
  created() {
    const Http = new XMLHttpRequest();
    const url = "https://glass-dry-erase.firebaseio.com/posts.json";
    namesRef.on('value', (snapshot) => {
      Http.open("GET", url);
      Http.send();
      Http.onreadystatechange = (e) => {
        if(Http.readyState === 4 && Http.status === 200) {
          console.log(Object.keys(JSON.parse(Http.response)).length)
          this.postId = Object.keys(JSON.parse(Http.response)).length;
          this.posts = JSON.parse(Http.response)
        }
      }
    })

  }
}
</script>
