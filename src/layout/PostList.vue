<template>
    <div v-if="posts.length > 0" class="posts">
      <div class="posts-content">
          <div
            v-for="post in posts"
            :post="post"
            :key="post.id"
            class="post-item"
          >
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
      </div>
      
  </div>
  <h2 v-else style="color: red">
    Список постов пуст
  </h2>
</template>

<script>
//import PostItem from "@/components/PostItem";
import axios from 'axios';

export default {
  //components: {PostItem},
  data(){
    return {
      posts: [],
    }
  },
  methods: {
    async fetchPosts(){
      try {
        var options = {
          year: 'numeric',
          month: 'long',
          day: 'numeric'
        };
        const response = await axios.get('https://mocki.io/v1/a5814d24-4e22-49fc-96d1-0e9ae2952afc');
        this.posts = response.data.articles;
        this.posts.forEach(row => {
                        let publishedAt = row['publishedAt'] ? (new Date(row['publishedAt'])).toLocaleDateString("ru", options) : ''; 
                        row['publishedAt'] = publishedAt;

                        let content = row['content'] ? row['content'].substring(0,200).concat('', '...') : '';
                        row['content'] = content;
                    }); 
      } catch (error) {
        console.log(error);
      }
    }
  },
  mounted() {
    this.fetchPosts();
  }
}
</script>

<style lang="scss" scoped>
.posts {
  background-color: $post-list_background-color;
  padding-bottom: 80px;
}

.posts-content {
  display: flex;
  flex-wrap: wrap;
  width: 90%;
  margin: auto;
  justify-content: space-between;
  
  min-height: 100%;
}

.post-item {
  width: 45%;
  display: flex;
  flex-direction: column;
  padding: 24px;
  border-radius: 10px;
  background-color: white;
}

.post-item + .post-item {
  margin-top: 20px;
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
  border-radius: 10px;
  padding: 8px 20px;
  
}

.post-item__title {
  font-weight: $post-list_title_font-weight;
  font-size: $post-list_title_font-size;
  line-height: $post-list_title_line-height;
  color: $post-list_title_text-color;
  margin-bottom: 30px;
}

.post-item__content {
  font-weight: $post-list_content_font-weight;
  font-size: $post-list_content_font-size;
  line-height: $post-list_content_line-height;
  color: $post-list_content_text-color;
  flex: 1 1 auto;
  margin-bottom: 25px;
}

.post-item__date {
  font-weight: $post-list_date_font-weight;
  font-size: $post-list_date_font-size;
  line-height: $post-list_date_line-height;
  color: $post-list_date_text-color;
  margin-bottom: 20px;
}
</style>