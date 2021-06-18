<template lang="html">
  <nav :style="{ background: background || '#333' }">
    <ul :style="{ background: background || '#333' }" ref="nav">
      <figure class="image-logo" @click="toggleNav">
        <img :src="imagePath" height="40px" width="40px" />
      </figure>
      <li
        v-for="(link, index) in navLinks"
        :Key="index"
        @mouseenter="
          $event.currentTarget.style.background = hoverbackground || '#999'
        "
        @mouseleave="
          $event.currentTarget.style.background = background || '#333'
        "
      >
        <router-link :to="link.path" :style="{ color: linkcolor || '#0f0' }">
          <i :class="link.icon" />
          {{ link.text }}
        </router-link>
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
  props: [
    "navLinks",
    "background",
    "linkcolor",
    "imagePath",
    "hoverbackground",
  ],
  methods: {
    toggleNav() {
      const nav = this.$refs.nav.classList;
      nav.contains("active") ? nav.remove("active") : nav.add("active");
    },
  },
};
</script>

<style scoped lang="scss">
* {
  box-sizing: border-box;
}
nav {
  height: 60px;
  width: 100%;
  box-shadow: 2px 2px 2px #0f0;

  ul {
    margin: 0;
    display: flex;
    height: 100%;
    align-items: center;
    box-shadow: 2px 2px 2px #0f0;

    figure {
      cursor: pointer;
      margin-right: 10px;
    }
    a {
      text-decoration: none;
      display: flex;
      flex-direction: row-reverse;
      align-items: center;
    }
    i {
      margin-left: 10px;
      font-size: 22px;
    }
    li {
      list-style-type: none;
      padding: 10px 20px;
    }
  }
}

@media screen and (max-width: 759px) {
  nav {
    ul {
      position: absolute;
      width: 300px;
      flex-direction: column;
      left: -240px;
      transition: 300ms ease all;
      top: 60px;

      &.active {
        left: 0px;
      }

      figure {
        position: fixed;
        z-index: 1;
        top: 1px;
        left: -24px;
      }

      li {
        width: 100%;
        padding-left: 0;
        padding-right: 0;
      }
      a {
        margin-left: 20px;
        justify-content: space-between;
        margin-right: 13px;
      }
    }
  }
}
</style>
