<template>
  <!-- <div class="card">
    <div class="card-header">
      <div class="card-title h5">{{ post.title }}</div>
      <div class="card-subtitle text-gray" v-if="post.subtitle">...</div>
    </div>
    <div class="card-body">
      {{ post.content }}
    </div>
    <div class="card-footer">
      <small>{{ post.date || `date goes here`}}</small>
    </div>
  </div> -->
  <div class="post">
    <h5>{{ post.title }}</h5>
    <hr>
    <div class="my-2">
      {{ post.content }}
    </div>
    <div class="my-2">
      <small><i>{{ post.date }}</i></small>
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
    }
  },
  data() {
    return {

    }
  }
}
</script>
