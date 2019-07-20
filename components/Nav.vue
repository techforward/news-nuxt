<template>
  <nav class="navbar" role="navigation" aria-label="main navigation">
    <div class="navbar-brand">
      <nuxt-link class="navbar-item" to="/">
        <p class="site-name">
          News.app
        </p>
      </nuxt-link>

      <a
        role="button"
        class="navbar-burger burger"
        :class="{ 'is-active': menuActive }"
        aria-label="menu"
        aria-expanded="false"
        data-target="navbarBasicExample"
        @click="menuToggle()"
      >
        <span aria-hidden="true" />
        <span aria-hidden="true" />
        <span aria-hidden="true" />
      </a>
    </div>

    <div
      id="navbarBasicExample"
      class="navbar-menu"
      :class="{ 'is-active': menuActive }"
    >
      <div class="navbar-start">
        <nuxt-link class="navbar-item" to="/about">
          このサイトについて
        </nuxt-link>
      </div>
      <a class="navbar-item">ランキング</a>
      <div class="navbar-item has-dropdown is-hoverable">
        <a class="navbar-link">Info</a>

        <div class="navbar-dropdown">
          <a class="navbar-item">About</a>
          <a class="navbar-item">Jobs</a>
          <hr class="navbar-divider" />
          <a class="navbar-item">Contact</a>
        </div>
      </div>

      <div class="navbar-end">
        <nuxt-link class="navbar-item" :to="{ name: 'settings' }">
          設定
        </nuxt-link>
        <div class="navbar-item">
          <div class="buttons">
            <a class="button is-primary">
              <strong>Sign up</strong>
            </a>
            <a class="button is-light">Log in</a>
          </div>
        </div>
      </div>
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
.navbar-item
  font-size: 1.2rem
  .site-name
    font-size: 1.5rem
</style>
