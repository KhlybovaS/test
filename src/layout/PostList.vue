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
      <post-item :filteredPosts="filteredPosts"/>
  </div>
  <h2 v-else class="posts__empty">
    Список постов пуст
  </h2>
</template>

<script>
import axios from 'axios';
import CustomSelect from "@/components/CustomSelect.vue";
import PostItem from "@/components/PostItem.vue";
import filterData from '@/utils/filter';

export default {
  components: {
    CustomSelect,
    'post-item': PostItem,
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
</style>