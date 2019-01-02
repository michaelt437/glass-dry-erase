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
      v-for="post in posts"
      :key="post.title"
      :post="post" />
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
    reset() {
      this.title = '';
      this.content = '';
      this.tagsInput = '';
    },
    post() {
      namesRef.child(this.postId).set({
        title: this.title,
        content: this.content,
        date: this.$moment().format('ll'),
        tags: this.tags
      });
      this.reset();
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
    }
  },
  created() {
    namesRef.on('value', (snapshot) => {
      console.log('the snapshot', JSON.stringify(snapshot.val(), null, 2))
      let postIdArr = Object.keys(snapshot.val());
      this.postId = postIdArr.length ?  postIdArr.length : 0;
      this.posts = snapshot.val().reverse();
    })
  }
}
</script>
