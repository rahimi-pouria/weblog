<template>
  <div class="nav navbarResponsive d-flex w-100 align-items-center">
    <!--  ham menu   -->
    <div class="ham-btn d-none flex-column g4 pointer" @click="sidebar = !sidebar">
      <div class="line" :class="{'line1':sidebar}" />
      <div class="line" :class="{'line2':sidebar}" />
      <div class="line" :class="{'line3':sidebar}" />
    </div>
    <transition name="nav">
      <div v-if="sidebar" class="nav-items d-none flex-column g60">
        <NuxtLink v-for="(item,index) in navMenu" :key="index" :to="item.path" class="pointer f14-700 c-title">
          {{ item.name }}
        </NuxtLink>
      </div>
    </transition>
    <NuxtLink to="/" class="LinkLogoModile">
      <img src="@/assets/img/logodeveloper.png" style="width: 66px;height: 53px" alt="">
    </NuxtLink>
    <NuxtLink to="" class="LinkLogoModile align-items-center">
      ورود
    </NuxtLink>
    <div class="container justify-content-between d-flex g32">
      <!--  logo    -->
      <NuxtLink to="/" class="d-flex navbarDesktop col-md-2 justify-content-center align-items-center">
        <img src="@/assets/img/logodeveloper.png" style="width: 66px;height: 53px" alt="">
      </NuxtLink>
      <!--      menu  -->
      <div class="d-flex align-items-center navbarDesktop w-100 col-md-8 g60">
        <NuxtLink
          v-for="(item , i) in navMenu"
          :key="i"
          :to="item.path"
          class="d-flex justify-content-start f20-400 g16"
        >
          {{ item.name }}
        </NuxtLink>
      </div>
      <div class="d-flex col-md-2 navbarDesktop align-items-center">
        <button class="btn-success" @click="modal = !modal">
          ورود
        </button>
      </div>
    </div>
    <div class="modal w-100" :class="{'hideModal':modal}">
      <div class="d-flex">
        <button @click="modal = !modal">
          Close
        </button>
      </div>
      <Modal />
    </div>
  </div>
</template>

<script>
import Modal from '~/components/Modal'
export default {
  name: 'NavLayout',
  components: { Modal },
  data () {
    return {
      sidebar: false,
      modal: true,
      navMenu: [
        {
          name: 'خانه',
          path: '/'
        },
        {
          name: 'محصولات',
          path: '/Product'
        },
        {
          name: 'خدمات',
          path: '/Service'
        },
        {
          name: 'وبلاگ',
          path: '/Blog'
        }
      ]
    }
  },
  methods: {
    CloseModal () {
      console.log('click modal')
      this.modal = false
    }
  }
}
</script>

<style scoped lang="scss">
  .line1{
    transform: translate(5px,5px) rotate(45deg);
  }
  .line2{
    display: none;
  }
  .line3{
    transform: translate(5px,-3px) rotate(-45deg);
  }
  .ham-btn{
    z-index: 110;
    width: 24px;
    height: max-content;
  }
  .line{
    transition: 300ms;
    border-radius: 12px;
    height: 4px;
    width: 100%;
    background: black;
  }
  .nav-items{
    position: fixed;
    z-index: 109;
    right: 0px;
    top: 0;
    height: 100%;
    align-items: center;
    padding: 86px 0;
    width: 180px;
    background: #03c855;
  }
  .nav{
      height: 65px;
  }
  .hideModal{
    display: none !important;
  }
  .modal{
    height: 100%;
    position: fixed;
    display: flex;
    align-items: center;
    justify-content: center;
    background: rgba(0, 0, 0, 0.3);
    flex-direction: column;
  }
  //responsive
  @media only screen and (max-width:800px){
    .nav-row{
      display: none !important;
    }
    .ham-btn, .nav-items{
      display: flex !important;
    }
    .navbarDesktop{
      display: none !important;
    }
    .navbarResponsive{
      justify-content: space-between;
      padding: 0 15px;
    }
  }
  @media only screen and (min-width:820px) and (max-width: 1180px) {
    .ham-btn, .nav-items{
      display: none !important;
    }
    .LinkLogoModile{
      display: none !important;
    }
  }
  @media only screen and (min-width:1200px){
    .ham-btn, .nav-items{
      display: none !important;
    }
    .LinkLogoModile{
      display: none !important;
    }
  }
</style>
