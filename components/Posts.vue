<template>
  <div class="d-flex text-center g16 flex-column g60">
    <h2 class="f32-700">
      وبلاگ
    </h2>
    <div class="d-flex position-relative align-items-center">
      <input
        v-model="search"
        type="text"
        placeholder="جستجو کنید..."
        class="form-control InputSearch align-items-center pt-2 pb-3 pr-5 f16-400 w-75"
        @input="Searches"
      >
      <img src="@/assets/img/search.png" class="position-absolute search" style="top: 7px; right: 5px" alt="">
    </div>
    <!--  show posts  -->
    <template v-for="(item, i) in postBlog">
      <div v-if="showData" :key="i" class="d-flex blogs flex-wrap w-100 bg-white">
        <img
          :src="item.introImageUrl.host"
          style="width: 254px; height: 288px;"
          alt=""
          class="col-md-4 col-sm-12 img-fluid photoBlog"
        >
        <div class="col-md-6 d-flex flex-column g4 text-right" style="max-height: 269px;">
          <h3 class="f16-500 titleBlog">
            {{ item.title }}
          </h3>
          <p class="f16-400 content" style="color: #373737">
            {{ item.body }}
          </p>
          <div class="d-flex justify-content-between w-100 responsivePosts">
            <div class="d-flex g4 justify-content-between align-items-center comment">
              <img src="@/assets/img/date.png" class="img-fluid photoData">
              <span class="f14-400">{{ item.createdAt }}</span>
            </div>
            <div class="d-flex g4 justify-content-between align-items-center comment">
              <img src="@/assets/img/comments.png" alt="">
              <span>{{ item.commentCount }}</span>
            </div>
            <div class="d-flex g4 justify-content-between align-items-center comment">
              <img src="@/assets/img/user.png" class="img-fluid photoData" alt="">
              <span class="f14-400">{{ item.author }}</span>
            </div>
          </div>
        </div>
        <div class="col-md-2 col-sm-12 d-flex align-items-end">
          <NuxtLink to="" class="btn-success btn-more-post d-flex justify-content-center f18-400 align-items-center">
            بیشتر
          </NuxtLink>
        </div>
      </div>
    </template>
    <template v-for="(item, index) in shows">
      <div :key="index" class="d-flex w-100 blogs bg-white">
        <img
          :src="item.introImageUrl.host"
          style="width: 254px; height: 288px;"
          alt=""
          class="col-md-4"
        >
        <div class="col-md-6 d-flex flex-column g4 text-right" style="max-height: 269px;">
          <h3 class="f18-500">
            {{ item.title }}
          </h3>
          <p class="f16-400 content" style="color: #373737">
            {{ item.body }}
          </p>
          <div class="d-flex g20">
            <div class="d-flex g8">
              <img src="@/assets/img/date.png">
              <span>{{ item.createdAt }}</span>
            </div>
            <div class="d-flex g8">
              <img src="@/assets/img/comments.png" alt="">
              <span>{{ item.commentCount }}</span>
            </div>
            <div class="d-flex g8">
              <img src="@/assets/img/user.png" alt="">
              <span>{{ item.author }}</span>
            </div>
          </div>
        </div>
        <div class="col-md-2 d-flex align-items-end">
          <NuxtLink to="" class="btn-success d-flex justify-content-center f18-400 align-items-center">
            بیشتر
          </NuxtLink>
        </div>
      </div>
    </template>
    <!-- show filter post   -->
    <template v-for="(post, index) in dataPost">
      <div v-if="posts" :key="index" class="d-flex blogs w-100 bg-white">
        <!--        <img-->
        <!--          :src="post.introImageUrl.host"-->
        <!--          style="width: 254px; height: 288px;"-->
        <!--          alt=""-->
        <!--          class="col-md-4"-->
        <!--        >-->
        <div class="col-md-6 d-flex flex-column g4 text-right" style="max-height: 269px;">
          <h3 class="f18-500">
            {{ post.title }}
          </h3>
          <p class="f16-400 content" style="color: #373737">
            {{ post.body }}
          </p>
          <div class="d-flex g12">
            <div class="d-flex g8">
              <img src="@/assets/img/date.png">
              <span>{{ post.createdAt }}</span>
            </div>
            <div class="d-flex g8">
              <img src="@/assets/img/comments.png" alt="">
              <span>{{ post.commentCount }}</span>
            </div>
            <div class="d-flex g8">
              <img src="@/assets/img/user.png" alt="">
              <span>{{ post.author }}</span>
            </div>
          </div>
        </div>
        <div class="col-md-2 d-flex align-items-end">
          <NuxtLink to="" class="btn-success d-flex justify-content-center f18-400 align-items-center">
            بیشتر
          </NuxtLink>
        </div>
      </div>
    </template>
  </div>
</template>

<script>
export default {
  name: 'PostsComponent',
  props: ['dataPost', 'posts', 'filtersData', 'showFilters'],
  data () {
    return {
      postBlog: [],
      search: null,
      shows: [],
      showData: true
    }
  },
  created () {
    fetch('https://challenge.webjar.ir/posts')
      .then(async (res) => {
        const post = await res.json()
        this.postBlog = post
      })
  },
  methods: {
    Searches () {
      this.shows = this.postBlog.filter(item => item.title.includes(this.search))
      this.showData = false
      console.log(this.showData)
    }
  }
}
</script>

<style scoped lang="scss">
.content {
  overflow: hidden;
  text-overflow: ellipsis;
  line-height: 2;
}  //responsive
@media only screen and (max-width:600px){
  .blogs{
    flex-wrap: wrap;
    gap: 15px;
  }
  .btn-more-post {
    width: 100% !important;
  }
  .responsivePosts {
    padding-bottom: 10px;
  }
  .photoBlog {
    width: 325px !important;
    height: 288px;
    border-radius: 10px;
  }
  .responsivePosts{
    padding-bottom: 15px;
    padding-top: 5px;
  }
  .search{
    top: 3px !important;
  }
  .InputSearch{
    padding-top: 10px !important;
  }
}
@media only screen and (min-width:820px) and (max-width: 1180px) {
}
@media only screen and (min-width:768px) and (max-width: 1024px){
}
@media only screen and (max-width: 320px){
  .photoBlog {
    width: 168px !important;
  }
  .responsivePosts{
    flex-wrap: wrap !important;
  }
}
</style>
