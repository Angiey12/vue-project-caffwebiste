<template>
  <div class="navbar-right">
    <!-- 已登录，显示用户信息 -->
    <ul v-if="auth" class="nav navbar-nav github-login">
      <li>
        <a v-dropdown href="javascript:;">
          <span v-if="user">
            <img v-if="user.avatar" :src="user.avatar" class="avatar-topnav">
            <span v-if="user.name">{{ user.name }}</span>
          </span>
          <span v-else>none</span>
          <span class="caret"></span>
        </a>
        <ul class="dropdown-menu">
          <!--编辑资料-->
          <li>
            <router-link to="/users/1/edit">
              <i class="fa fa-cog text-md i-middle"></i>
              Edit File
            </router-link>
          </li>

          <li><a href="javascript:" @click="logout"><i class="fa fa-sign-out text-md"></i>Logout</a></li>
        </ul>
      </li>
    </ul>
    <!-- 未登录，显示登录注册 -->
    <div v-else class="nav navbar-nav github-login">
      <router-link to="/auth/login" class="btn btn-default login-btn">
        <i class="fa fa-user"></i> Login
      </router-link>
      <router-link to="/auth/register" class="btn btn-default login-btn">
        <i class="fa fa-user-plus"></i> Signup
      </router-link>
    </div>
  </div>
</template>

<script>
// 引入 mapState 辅助函数
import { mapState } from 'vuex'

export default {
  name: 'TheEntry',
  // 添加计算属性选项
  computed: {
    // 使用对象展开运算符，将 mapState 对象混入到计算属性之中
    ...mapState([
      // 映射 this.auth 为 store.state.auth
      'auth',
      // 映射 this.user 为 store.state.user
      'user'
    ])
  },
  // 添加 methods 选项，并添加 logout 方法
  methods: {
    logout() {
      this.$store.dispatch('logout')
    }
  }
}
</script>

<style scoped>

</style>