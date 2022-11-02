<template>
  <div class="posts-content">
    <transition-group name="post-list">
      <div v-for="post in filteredPosts"
                :key="post.id"
                class="post-item"
      >
        <div class="post-item__date">
          {{ post.publishedDate }}
        </div>
        <div class="post-item__title">
          {{ post.title }}
        </div>
        <div class="post-item__content">
          {{ post.contentCut }}
        </div>
        <div class="post-item__author">
        <div class="post-item__author_content">
          {{ post.author }}
        </div>
        </div>
      </div>  
    </transition-group> 
  </div>  
</template>

<script>
export default {
  name: 'post-item',
  props: {
    filteredPosts: {
      type: Object,
      required: true,
    }
  }
}
</script>

<style lang="scss" scoped>

.posts-content {
  display: flex;
  flex-wrap: wrap;
  width: $content-width;
  margin: auto;
  justify-content: space-between;
  min-height: 100%;

:hover {
    //box-shadow: 0 14px 28px rgba(0,0,0,0.25), 0 10px 10px rgba(0,0,0,0.22);
    cursor: pointer;
  }
}

.post-item {
  width: 45%;
  display: flex;
  flex-direction: column;
  padding: 24px;
  border-radius: $border-radius;
  background-color: white;
  margin-bottom: 20px;

  @media (max-width: $breakpoint_desktop) {
    width: 40%;
  }

  @media (max-width: $breakpoint_tablet) {
    width: $content-width;
    padding: 20px;
  }
}

.post-item__author {
  display: flex;
}

.post-item__author_content {
  font-weight: $post-list_author_font-weight;
  font-size: $post-list_author_font-size;
  line-height: $post-list_author_line-height;
  color: $post-list_author_text-color;
  background-color: $post-list_author_background-color;
  border-radius: $border-radius;
  padding: 8px 20px;
}

.post-item__title {
  font-weight: $post-list_title_font-weight;
  font-size: $post-list_title_font-size;
  line-height: $post-list_title_line-height;
  color: $post-list_title_text-color;
  margin-bottom: 30px;

  @media (max-width: $breakpoint_tablet) {
    font-size: $post-list_title_font-size-mobile;
    line-height: $post-list_title_line-height-mobile;
  }
}

.post-item__content {
  font-weight: $post-list_content_font-weight;
  font-size: $post-list_content_font-size;
  line-height: $post-list_content_line-height;
  color: $post-list_content_text-color;
  flex: 1 1 auto;
  margin-bottom: 25px;

  @media (max-width: $breakpoint_tablet) {
    font-size: $post-list_content_font-size-mobile;
    line-height: $post-list_content_line-height-mobile;
  }
}

.post-item__date {
  font-weight: $post-list_date_font-weight;
  font-size: $post-list_date_font-size;
  line-height: $post-list_date_line-height;
  color: $post-list_date_text-color;
  margin-bottom: 20px;
}

.post-list-enter-active,
.post-list-leave-active {
  transition: all 0.4s ease;
}

.post-list-enter-from,
.post-list-leave-to {
  opacity: 0;
  transform: translateX(130px);
}

.post-list-move {
  transition: all 0.4s ease;
}
</style>