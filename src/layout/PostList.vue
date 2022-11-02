<template>
    <div v-if="posts.length > 0" class="posts">
      <div class="posts__filter-section">
        <CustomSelect
                v-model="selectedFilter"
                :options="options"
        />
        <div class="posts__filter-section_content">
          <label for="selectedDateBegin" class="posts__filter-section_label-begin"
          >
            От
          </label>
          <input 
            type="date" 
            class="posts__filter-section_date-begin" 
            v-model="selectedDateBegin" id="selectedDateBegin"
          >
          <label      
            for="selectedDateEnd"
            class="posts__filter-section_label-end"
          >
            &ndash; До
          </label>
          <input 
            type="date" 
            class="posts__filter-section_date-end" 
            v-model="selectedDateEnd" 
            id="selectedDateEnd"
          >
        </div>
      </div>
      <div class="posts-content">
        <transition-group name="post-list">
          <div
            v-for="post in filteredPosts"
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
  </div>
  <h2 v-else class="posts__empty">
    Список постов пуст
  </h2>
</template>

<script>
import axios from 'axios';
import CustomSelect from "@/components/CustomSelect.vue";
import filterData from '@/utils/filter';

export default {
  components: {
    CustomSelect,
  },
  data(){
    return {
      posts: [],
      options: [],
      selectedFilter: '',
      selectedDateBegin: false,
      selectedDateEnd: false,
    }
  },
  methods: {
    async fetchPosts(){
      try {
        var params = {
          year: 'numeric',
          month: 'long',
          day: 'numeric'
        };
        const response = await axios.get('https://mocki.io/v1/a5814d24-4e22-49fc-96d1-0e9ae2952afc');
        this.posts = response.data.articles;
        this.posts.forEach(row => {
                        let publishedDate = row['publishedAt'] ? (new Date(row['publishedAt'])).toLocaleDateString("ru", params) : ''; 
                        row['publishedDate'] = publishedDate;

                        let contentCut = row['content'] ? row['content'].substring(0,200).concat('', '...') : '';
                        row['contentCut'] = contentCut;

                        let author = row['author'] ? row['author'] : 'Without author';
                        row['author'] = author;
                    }); 
        this.options = response.data.articles;
        var i = 1;
        this.options.forEach(row=> {
          let name = row['author'] ? row['author'] : 'Without author';
          row['name'] = name;
          
          let value = row['author'] ? row['author'] : 'Without author';
          i = i + 1;
          row['value'] = value;
        });
        this.options =  filterData(this.options.sort((a, b) => a.name > b.name ? 1 : -1), 'name');
      } catch (error) {
        console.log(error);
      }
    }
  },
  mounted() {
    this.fetchPosts();
  },
  computed: {
    filteredPosts() {
      return this.posts.filter(post => post.author.toLowerCase().includes(this.selectedFilter.toLowerCase()))
        .filter(post => {
          if (this.selectedDateBegin && this.selectedDateEnd) {
              return (new Date(post.publishedAt)) >= (new Date(this.selectedDateBegin)) 
            && (new Date(post.publishedAt)) <= (new Date(this.selectedDateEnd))
            }

          if (this.selectedDateBegin && !this.selectedDateEnd) {
              return (new Date(post.publishedAt)) >= (new Date(this.selectedDateBegin))
          }

          if (!this.selectedDateBegin && this.selectedDateEnd) {
              return (new Date(post.publishedAt)) <= (new Date(this.selectedDateEnd))
          }
          
          return true;
    })},
  }
}
</script>

<style lang="scss" scoped>
.posts {
  background-color: $post-list_background-color;
  padding-bottom: 80px;

  @media(max-width: $breakpoint_mobile){
    padding-bottom: 55px;
  }
}

.posts__empty {
  width: $content-width;
  margin: auto;
  padding-top: 20px;
  padding-bottom: 20px;
}

.posts-content {
  display: flex;
  flex-wrap: wrap;
  width: $content-width;
  margin: auto;
  justify-content: space-between;
  min-height: 100%;

:hover {
    box-shadow: 0 14px 28px rgba(0,0,0,0.25), 0 10px 10px rgba(0,0,0,0.22);
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

  :hover {
    box-shadow: none;
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

.posts__filter-section {
  display: flex;
  width: $content-width;
  margin: auto;
  padding-top: 40px;
  padding-bottom: 40px;
  position: sticky;
  top: 78px;
  background-color: rgba(229,229,229,.8);
  
  @media( max-width: $breakpoint_tablet){
    flex-direction: column;
    top: 46px;
  }
}

.posts__filter-section_label-begin {
  background-color: white;
  border-top-left-radius: $border-radius;
  border-bottom-left-radius: $border-radius;
  display: flex;
  align-items: center;
  padding: 10px;
  margin-left: 20px;
  color: #888888;
  font-weight: 600;
  font-size: 1.1rem;

  @media( max-width: $breakpoint_tablet){
    margin-left: 0;
    font-size: 1rem;
    flex-grow: 1;
  }

  @media( max-width: $breakpoint_mobile){
    font-size: 0.7rem;
    padding: 5px;
  }
}

.posts__filter-section_label-end {
  background-color: white;
  display: flex;
  align-items: center;
  padding: 10px;
  color: #888888;
  font-weight: 600;
  font-size: 1.1rem;

  @media( max-width: $breakpoint_tablet){
    font-size: 1rem;
    flex-grow: 1;
  }

  @media( max-width: $breakpoint_mobile){
    font-size: 0.7rem;
    padding: 5px;
  }
}

.posts__filter-section_date-begin, .posts__filter-section_date-end {
  border: none;
}

.posts__filter-section_date-end {
  border-top-right-radius: $border-radius;
  border-bottom-right-radius: $border-radius;
  padding-right: 10px;
  padding: 16px;

  @media( max-width: $breakpoint_tablet){
    flex-grow: 1;
  }

   @media( max-width: $breakpoint_mobile){
    padding-left: 5px;
    padding-right: 5px;
    font-size: 0.7rem;
  }
}

.posts__filter-section_date-begin {
  @media( max-width: $breakpoint_tablet){
    flex-grow: 1;
  }

   @media( max-width: $breakpoint_mobile){
    padding-left: 5px;
    padding-right: 5px;
    font-size: 0.7rem;
  }
}

.posts__filter-section_content {
  display: flex;
  min-height: 2em;

  @media( max-width: $breakpoint_tablet){
    width: $content-width;
  }
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