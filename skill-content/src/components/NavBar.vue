<template>
  <el-menu
    v-bind:default-active="active_index"
    mode="horizontal"
    @select="handleSelect"
    class="nav-menu"
  >
    <burger class="nav-menu-burger" :is_burger_active="is_burger_active">
    </burger>
    <a
      class="logo"
      href="/skill-content/dist/"
      style="cursor: pointer;outline:none;"
    >
      <img
        src="/favicon.ico"
        style="float: left; margin-left: 35px; margin-top: 10px; width: 40px;height: 40px;"
      />
    </a>
    <el-submenu
      v-for="cont in contents.filter(cont => cont['contents'].length)"
      v-bind:key="cont['title']"
      v-bind:index="cont['title']"
      class="nav-menu-item"
    >
      <template slot="title">{{ cont["title"] }}</template>
      <el-menu-item
        v-for="subcont in cont['contents']"
        v-bind:key="cont['title'] + '-' + subcont['title']"
        v-bind:index="cont['title'] + '-' + subcont['title']"
      >
        {{ subcont["title"] }}
      </el-menu-item>
    </el-submenu>
    <el-menu-item
      v-for="cont in contents.filter(cont => !cont['contents'].length)"
      v-bind:key="cont['title']"
      v-bind:index="cont['title']"
      class="nav-menu-item"
    >
      {{ cont["title"] }}
    </el-menu-item>
    <el-menu-item index="blog" class="nav-menu-blog">
      博客
    </el-menu-item>
  </el-menu>
</template>

<script>
import burger from "@/components/Burger.vue";

export default {
  name: "navbar",
  components: {
    burger
  },
  methods: {
    handleSelect(key) {
      if (key == "blog") {
        location.href = "/?mode=blog";
      } else {
        this.$store.commit("setNavigationSelectedIndex", key);
      }
    }
  },
  props: {
    contents: {
      type: Array,
      default: () => []
    },
    active_index: {
      type: String,
      required: true
    },
    is_burger_active: {
      type: Boolean,
      required: true
    }
  }
};
</script>

<style lang="stylus" scoped>
.nav-menu-item
  float right
.nav-menu-burger
  float left
  visibility hidden
@media screen and (max-width: 900px)
  .nav-menu-burger
    visibility visible
  .nav-menu-item
    display none
  .logo
    position absolute
    right 45%
.nav-menu-blog
  float right
  color RoyalBlue
  font-size 18px
  font-family: "Gill Sans", sans-serif;
</style>
