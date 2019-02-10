<template>
  <div class="post">
    <h5>{{ post.title }}</h5>
    <hr>
    <div class="post__content my-2" v-html="contentReturn">
    </div>
    <div class="post__footer my-2">
      <small><i>{{ post.date }}</i></small>
      <div class="flex-spacer"></div>
      <i class="icon icon-delete" @click="$emit('deletePost', postId)"></i>
    <!-- <div class="post__date my-2">
      <small>{{ post.date }}</small>
    </div>
    <div class="post__tags my-2" v-if="post.tags">
      <span
        class="chip"
        v-for="tag in post.tags"
        :key="tag">
          {{ tag }}
      </span> -->
    </div>
  </div>
</template>

<script>
export default {
  name: 'dry-erase-post',
  props: {
    post: {
      type: Object,
      required: true
    },
    postId: {
      type: Number,
      required: false
    }
  },
  data() {
    return {

    }
  },
  computed: {
    contentReturn() {
      let r = this.post.content.replace('\n', '<br>')
      return r
    }
  }
}
</script>
