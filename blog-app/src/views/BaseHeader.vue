<template>
  <el-header class="me-area">
    <el-row class="me-header">
      <el-col :span="4" class="me-header-left">
        <router-link to="/" class="me-title">
          <img src="../assets/img/logo.png">
        </router-link>
      </el-col>

      <el-col v-if="!simple" :span="16">
        <el-menu
          :router="true"
          menu-trigger="click"
          active-text-color="#5FB878"
          :default-active="activeIndex"
          mode="horizontal"
        >
          <el-menu-item index="/">首页</el-menu-item>
          <el-menu-item index="/category/all">文章分类</el-menu-item>
          <el-menu-item index="/tag/all">标签</el-menu-item>
          <el-menu-item index="/archives">文章归档</el-menu-item>
          <el-menu-item index="/log">日志</el-menu-item>
          <el-menu-item index="/messageBoard">留言板</el-menu-item>

          <el-col :span="4" :offset="4">
            <el-menu-item index="/write">
              <i class="el-icon-edit"></i>写文章
            </el-menu-item>
          </el-col>
        </el-menu>
      </el-col>

      <template v-else>
        <slot></slot>
      </template>

      <el-col :span="4">
        <el-menu :router="true" menu-trigger="click" mode="horizontal" active-text-color="#5FB878">
          <template v-if="!user.login">
            <el-menu-item index="/login">
              <el-button type="text">登录</el-button>
            </el-menu-item>
            <el-menu-item index="/register">
              <el-button type="text">注册</el-button>
            </el-menu-item>
          </template>

          <template v-else>
            <!-- <el-menu
              :default-active="activeIndex"
              class="el-menu-demo"
              mode="horizontal"
              @select="handleSelect"
            >
              <el-submenu index="2">
                <template slot="title">
                  <img class="me-header-picture" :src="user.avatar">
                </template>
                <el-menu-item index="2-1" @click="logout">
                  <i class="el-icon-back"></i>退出
                </el-menu-item>
                <el-menu-item index="2-2">我的博客</el-menu-item>
              </el-submenu>
            </el-menu>-->

            <el-dropdown placement="bottom" @command="onSelected">
              <span class="el-dropdown-link">
                <div class="userSelect-container">
                  <img class="me-header-picture" :src="user.avatar">
                  <span>{{user.name}}</span>
                </div>
              </span>
              <el-dropdown-menu slot="dropdown">
                <el-dropdown-item command="logout">退出</el-dropdown-item>
                <el-dropdown-item command="own">个人中心</el-dropdown-item>
              </el-dropdown-menu>
            </el-dropdown>
          </template>
        </el-menu>
      </el-col>
    </el-row>
  </el-header>
</template>

<script>
export default {
  name: "BaseHeader",
  props: {
    activeIndex: String,
    simple: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {};
  },
  computed: {
    user() {
      let login = this.$store.state.account.length != 0;
      let avatar = this.$store.state.avatar;
      let name = this.$store.state.name;
      return {
        login,
        avatar,
        name
      };
    },
    handleSelect(key, keyPath) {
      console.log(key, keyPath);
    }
  },
  methods: {
    onSelected(val) {
      if (val === "logout") {
        this.logout();
      }

      if (val === "own") {
        this.$router.push({ path: `/own` });
      }
    },
    logout() {
      let that = this;
      this.$store
        .dispatch("logout")
        .then(() => {
          this.$router.push({ path: "/" });
        })
        .catch(error => {
          if (error !== "error") {
            that.$message({ message: error, type: "error", showClose: true });
          }
        });
    }
  }
};
</script>

<style>
.el-header {
  position: fixed;
  z-index: 1024;
  min-width: 100%;
  box-shadow: 0 2px 3px hsla(0, 0%, 7%, 0.1), 0 0 0 1px hsla(0, 0%, 7%, 0.1);
}

.me-title {
  margin-top: 10px;
  font-size: 24px;
}

.me-header-left {
  margin-top: 10px;
}

.me-title img {
  max-height: 2.4rem;
  max-width: 100%;
}

.me-header-picture {
  width: 36px;
  height: 36px;
  border: 1px solid #ddd;
  border-radius: 50%;
  vertical-align: middle;
  background-color: #5fb878;
}
.el-dropdown-link {
  cursor: pointer;
  color: #409eff;
}
.el-icon-arrow-down {
  font-size: 12px;
}
</style>
