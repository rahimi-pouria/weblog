<template>
  <div class="d-flex p-5 g32 flex-column bg-white justify-content-center align-items-center w-50 text-center rounded">
    <h3 class="f18-700 p-2">
      ورود به حساب کاربری
    </h3>
    <div class="form-group forms">
      <label class="f18-700">نام کاربری</label>
      <input type="text" class="form-control login" placeholder="نام کاربری خود را وارد کنید">
    </div>
    <div class="form-group forms">
      <label class="f18-700">رمز عبور</label>
      <input type="password" class="form-control login" placeholder="رمز عبور خود را وارد کنید">
    </div>
    <button class="btn-success" @click="getdata">
      ورود
    </button>
  </div>
</template>

<script>
export default {
  name: 'ModalComponent',
  data () {
    return {
      users: []
    }
  },
  methods: {
    getdata () {
      fetch('https://challenge.webjar.ir/auth/login')
        .then(async (res) => {
          const login = await res.json()
          this.users = login
          console.log(this.users)
        })
    }
  }
}
</script>

<style scoped lang="scss">
  .forms{
    width: 60%;
    text-align: right;
  }
  .login{
    padding: 25px;
    display: flex;
    align-items: center;
    border: 1px solid rgba(0, 0, 0, 0.2);
    border-radius: 15px;
  }
</style>
