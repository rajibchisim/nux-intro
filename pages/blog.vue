<template>
  <article>
    <h1>{{ page.title }}</h1>
    <nuxt-content :document="page" />
  </article>
</template>

<script>
export default {
  async asyncData ({ $content }) {
    const page = await $content('posts/new-post').fetch()
    const pageDebug = await $content('posts')
                                  .where({ category : 'post' }).fetch()
    console.log(pageDebug)

    return {
      page
    }
  }
}
</script>

<style>

</style>
