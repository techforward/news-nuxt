<template>
  <div class="container">
    <div class="categories">
      <div
        v-for="(category, index) in categories"
        :key="category"
        class="category-link"
      >
        <p v-if="index !== 0" class="divide">
          /
        </p>
        <nuxt-link
          class="category"
          :to="{ name: 'category-name', params: { name: category } }"
        >
          {{ category }}
        </nuxt-link>
      </div>
    </div>
    <div class="columns is-multiline is-vcentered">
      <div
        v-for="(article, index) in newsData"
        :key="article.publishedAt"
        :class="[
          'column',
          index === 0 || index === 6 || index === 13 || index === 19
            ? 'is-two-thirds-desktop is-two-thirds-tablet'
            : 'is-one-thirds-desktop is-one-third-tablet'
        ]"
      >
        <a :href="article.url">
          <div class="card">
            <div class="card-image">
              <figure
                :class="[
                  'image',
                  index === 0 || index === 6 || index === 13 || index === 19
                    ? 'is-3by1'
                    : 'is-3by2'
                ]"
              >
                <img :src="article.urlToImage" alt="Placeholder image" />
              </figure>
            </div>
            <div class="card-content">
              <div class="content">
                <p class="content-title subtitle">{{ article.title }}</p>
                <time :datetime="article.publishedAt">{{
                  article.publishedAt
                }}</time>
              </div>
            </div>
          </div>
        </a>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data: function() {
    return {
      categories: [
        'business',
        'entertainment',
        'general',
        'health',
        'science',
        'sports',
        'technology'
      ]
    }
  },
  async asyncData(context) {
    const url =
      'http://localhost:3000/api/v2/top-headlines?' +
      'country=jp&' +
      'category=' +
      context.params.name +
      '&' +
      'apiKey=43e584e514174783ac4c7b0975951259'
    const data = await context.app.$axios.$get(url, {
      headers: {
        'Content-Type': 'application/json',
        'Access-Control-Allow-Origin': '*'
      },
      data: {}
    })
    return {
      newsData: data.articles
    }
  }
}
</script>

<style lang="sass" scoped>
.container
  margin: 0 auto
  padding: 2rem
  min-height: 100vh
.categories
  Width: 100%
  display: flex
  justify-content: flex-start
  font-size: 1.4rem
  .category-link
    display: inline-flex
    .category
      padding-right: 0.7rem
      padding-bottom: 0.7rem
    .divide
      padding-right: 0.7rem
.card-image
  overflow: hidden
  .image
    img
      object-fit: cover
.content-title
  height: 50px
  font-weight: bold
  overflow: hidden
  text-overflow: ellipsis
</style>
