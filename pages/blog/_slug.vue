<template>
  <article>
    <p>Post last updated: {{ formatDate(article.updatedAt) }}</p>
    <p>Table of contents:</p>
    <nav>
      <ul>
        <li v-for="link of article.toc" :key="link.id">
          <NuxtLink :to="`#${link.id}`" :class="{ 'py-2': link.depth === 2, 'ml-2 pb-2': link.depth === 3 }">{{ link.text }}</NuxtLink>
        </li>
      </ul>
    </nav>
    <nuxt-content :document="article" />
    <!-- <pre> {{ article }} </pre> -->
  </article>
</template>

<script>
export default {
    async asyncData({ $content, params }) {
        const article = await $content('articles', params.slug).fetch()

        return { article }
    },
    methods: {
        formatDate(date) {
        const options = { year: 'numeric', month: 'long', day: 'numeric' }
        return new Date(date).toLocaleDateString('en', options)
        }
    }

}
</script>

<style>
  .nuxt-content h1 {
    font-weight: bold;
    font-size: 28px;
    text-indent: 0em; 
  }
  .nuxt-content h2 {
    font-weight: bold;
    font-size: 28px;
  }
  .nuxt-content h3 {
    font-weight: bold;
    font-size: 22px;
  }
  .nuxt-content p {
    margin-bottom: 20px;
  }
  .icon.icon-link {
  background-image: url('~assets/album.svg');
  display: inline-block;
  width: 20px;
  height: 20px;
  background-size: 20px 20px;
  }
  .bg-blue-500 {
    background-color: blue;
  }
  .text-white {
    color: white;
  }
  .p-4 {
    padding-left: 4em;
  }
  .mb-4 {
    margin-bottom: 4em;
  }

</style>
