<template>
    <div>
        <div class="post" 
            v-for="post in posts" 
            :key="post.id"
        >
            <div class="post__author">
                {{ post.author }}
            </div>
            <div class="post__title">
                    {{ post.title }}
            </div>
            <div class="post__content">
                    {{ post.content }}
            </div>
        </div>
    </div> 
</template>

<script>
export default {
  props: {
    post: {
      type: Object,
      required: true,
    }
  }
}
</script>