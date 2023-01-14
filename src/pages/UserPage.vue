<template>
  <div>
    <h1 class="title">Posts</h1>
    <my-input 
      v-model="searchQuery"
      placeholder="Search"
    />
    <div class="app__btns">
      <my-button
        @click="showDialog"
      >
        Create
      </my-button>
      <my-select 
        v-model="selectedSort"
        :options="sortOptions"
      />
    </div>
    
    <my-dialog v-model:show="dialogVisible">
      <post-form 
      @create="createPost"
    />
    </my-dialog>
    
    <post-list
      :posts="sortedAndSearchedPosts" 
      @remove="removePost"
      v-if="!isPostsLoading"
    />
    <div v-else >Loading..</div>
    <div ref="observer" class="observer">

    </div>
    <!-- <div class="page__wrapper">
      <div 
        class="page"
        v-for="pageNumber in totalPages"
        :key="page"
        :class="{
          'current-page': page === pageNumber 
        }"
        @click="changePage(pageNumber)"
      > 
        {{ pageNumber }}
      </div>
    </div> -->
  </div>
</template>

<script>
import PostForm from "@/components/PostForm"
import PostList from "@/components/PostList"
import axios from 'axios'
  export default {
    components: {
      PostForm,
      PostList
    },  
    data() {
      return {
        posts: [],
        dialogVisible: false,
        isPostsLoading: false,
        selectedSort: '',
        searchQuery: '',
        page: 1,
        limit: 10,
        totalPages: 0,
        sortOptions: [
          {value: 'title', name: 'name'},
          {value: 'body', name: 'description'},
        ]
      }
    },
    methods: {
      createPost(post) {
        this.posts.push(post);
        this.dialogVisible = false;
      },
      removePost(post) {
        this.posts = this.posts.filter(p => p.id !== post.id);
      },
      showDialog() {
        this.dialogVisible = true;
      },
      // changePage(pageNumber) {
      //   this.page = pageNumber;
      // },  
      async fetchPosts() {
        try {
          const response = await axios.get(`https://jsonplaceholder.typicode.com/posts`, {
            params: {
              _page: this.page,
              _limit: this.limit,
            }
          });
          this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit);
          this.posts = response.data;
        } catch (e) {
          alert('error');
        } finally {
          this.isPostsLoading = false;
        }
      },
      async loadMorePosts() {
        try {
          this.page += 1;
          const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
            params: {
              _page: this.page,
              _limit: this.limit,
            }
          });
          this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit);
          this.posts = [...this.posts, ...response.data];
        } catch (e) {
          alert('error');
        } finally {
        }
      },
    },
    mounted() {
      this.fetchPosts();
      console.log(this.$refs.observer)
      let options = {
        rootMargin: '0px',
        threshold: 1.0
      };
      let callback = (entries, observer) => {
        if(entries[0].isIntersecting && this.page < this.totalPages) {
          this.loadMorePosts()
        }
      };
      let observer = new IntersectionObserver(callback, options);
      observer.observe(this.$refs.observer);
    },   
    computed: {
      sortedPosts() {
        return [...this.posts].sort((post1, post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]))
      },  
      sortedAndSearchedPosts() {
        return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
      },
    },
    watch: {
      // page() {
      //   this.fetchPosts()
      // }
    }
  }
</script>

<style scoped>
.title {
  text-align: center;
}
.app__btns {
  margin: 15px 0;
  display: flex;
  justify-content: space-between;
}
.page__wrapper {
   display: flex;
   justify-content: center;
   margin-top: 15px;
}
.page {
  border: 1px solid #000;
  padding: 5px 10px;
  margin: 0 5px;
}
.current-page {
  border: 2px solid teal;
  transform: translateY(-3px);
}
.observer {
  height: 30px;
  background-color: teal;
  margin-top: 15px;
}
</style>

// single file component 