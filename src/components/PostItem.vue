<template>
<div>
  <div class="post-item__date">
                    {{ post.publishedAt }}
            </div>
            <div class="post-item__title">
                    {{ post.title }}
            </div>
            <div class="post-item__content">
                    {{ post.content }}
            </div>
            <div class="post-item__author">
              <div class="post-item__author_content">
                    {{ post.author }}
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