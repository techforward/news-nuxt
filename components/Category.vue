<template>
  <nav class="navbar" role="navigation" aria-label="main2 navigation">
    <div class="navbar-brand">
      <!-- <p class="site-name" :class="{ 'is-active': !menuActive }">
        カテゴリー
      </p>-->
      <a
        role="button"
        class="navbar-burger burger"
        :class="{ 'is-active': menuActive }"
        aria-label="menu2"
        aria-expanded="false"
        data-target="navbarBasicExample2"
        @click="menuToggle()"
      >
        <span aria-hidden="true" />
        <span aria-hidden="true" />
        <span aria-hidden="true" />
      </a>
    </div>

    <div
      id="navbarBasicExample2"
      class="navbar-menu"
      :class="{ 'is-active': menuActive }"
    >
      <div class="navbar-start">
        <nuxt-link class="navbar-item" to="/about">
          スポーツ
        </nuxt-link>
        <nuxt-link class="navbar-item" to="/about">
          政治
        </nuxt-link>
        <nuxt-link class="navbar-item" to="/about">
          科学
        </nuxt-link>
      </div>

      <div class="navbar-end" />
    </div>
  </nav>
</template>
<script>
export default {
  components: {},
  data() {
    return {
      menuActive: false
    }
  },
  methods: {
    menuToggle() {
      this.menuActive = !this.menuActive
    }
  }
}
</script>
<style lang="sass" scoped>
.navbar
  padding: 0 2rem
.navbar-item
  font-size: 1.2rem
</style>
