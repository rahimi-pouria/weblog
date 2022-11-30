<template>
  <div class="container-Blog d-flex flex-column g60">
    <div class="d-flex w-100 g4" style="padding-right: 50px;">
      <span>خانه</span>
      <span> > </span>
      <span>{{ location }}</span>
    </div>
    <button class="w-100 f16-700 closeSideBarResponsive" @click="showSide">
      دسته بندی
    </button>
    <div class="d-flex Body-Blog">
      <div class="col-md-3 col-sm-12" :class="{'showCat': showSideBar}" style="padding-top: 10rem !important;">
        <div class="d-flex flex-column  w-100" style="padding: 30px 10px">
          <div v-for="(cat ,i) in category" :key="i" class="d-flex justify-content-between">
            <label>{{ cat.name }}</label>
            <input type="checkbox" @click="FilterPosts">
          </div>
        </div>
      </div>
      <div class="col-lg-9 col-md-12 text-right" id="responsiveTablete">
        <Posts :dataPost="FilterPost"
               :filtersData="FilterPosts"
               :showpost="showData"
               :posts="shoowFilterPost"
               :Search="Searches"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Posts from '~/components/Posts'
export default {
  name: 'Blog',
  components: { Posts },
  layout: 'Navbar',
  data () {
    return {
      category: [],
      FilterPost: [],
      shoowFilterPost: false,
      showData: true,
      location: null,
      showSideBar: true
    }
  },
  methods: {
    FilterPosts () {
      fetch('https://challenge.webjar.ir/post-categories/{id}')
        .then(async (res) => {
          const filters = await res.json()
          this.FilterPost = filters
          this.showData = false
          this.shoowFilterPost = true
        })
    },
    Searches () {
      this.shows = this.postBlog.filter(item => item.title.includes(this.search))
      this.showData = false
    },
    showSide () {
      const AddClass = document.getElementById('responsiveTablete')
      if (this.showSideBar === false) {
        AddClass.classList.add('col-md-12')
        AddClass.classList.remove('col-md-9')
      } else {
        AddClass.classList.add('col-md-9')
        AddClass.classList.remove('col-md-12')
      }
      this.showSideBar = !this.showSideBar
    }
  },
  mounted () {
    this.location = this.$nuxt.$route.name
    console.log(this.location)
  },
  created () {
    fetch('https://challenge.webjar.ir/post-categories')
      .then(async (res) => {
        const cat = await res.json()
        this.category = cat
      })
  }
}
</script>

<style scoped lang="scss">
.WrapBlog{
  flex-wrap: wrap !important;
}
//responsive
@media only screen and (max-width:800px){
  .showCat{
    display: none !important;
  }
  .closeSideBarResponsive {
    background: #00c853 !important;
    color: #fff !important;
    padding: 10px 0 !important;
    border-radius: 15px !important;
    border: none !important;
  }
}
@media only screen and (max-width:800px){
  .Body-Blog{
    flex-wrap: wrap;
  }
}
@media only screen and (min-width:820px) and (max-width: 1180px) {
  label {
    text-align: right !important;
  }
  .showCat{
    display: none !important;
  }
}
@media only screen and (min-width:768px) and (max-width: 1024px){
  label {
    text-align: right !important;
  }
  .showCat{
    display: none !important;
  }
}
@media only screen and (min-width:1200px){
  .closeSideBarResponsive {
    display: none;
  }
}
</style>
