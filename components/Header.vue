<template>
    <div>
      <!-- Text Header -->
      <header class="w-full container mx-auto">
          <div class="flex flex-col items-center py-12">
              <a class="font-bold text-gray-800 uppercase hover:text-gray-700 text-5xl" href="#">
                  Minimal Blog
              </a>
              <p class="text-lg text-gray-600">
                  Lorem Ipsum Dolor Sit Amet
              </p>
          </div>
      </header>
      <!-- Topic Nav -->
      <nav class="w-full py-4 border-t border-b bg-gray-100" x-data="{ open: false }">
          <div class="block sm:hidden">
              <a
                  href="#"
                  class="block md:hidden text-base font-bold uppercase text-center flex justify-center items-center"
                  @click="open = !open"
              >
                  Topics <i :class="open ? 'fa-chevron-down': 'fa-chevron-up'" class="fas ml-2"></i>
              </a>
          </div>
          <div :class="open ? 'block': 'hidden'" class="w-full flex-grow sm:flex sm:items-center sm:w-auto">
              <div class="w-full container mx-auto flex flex-col sm:flex-row items-center justify-center text-sm font-bold uppercase mt-0 px-6 py-2">
                  <a href="#"
                      class="hover:bg-gray-400 rounded py-2 px-4 mx-2"
                      v-for="tag in tags" v-bind:key="tag"
                  >{{ tag }}</a>
              </div>
          </div>
      </nav>
    </div>
</template>

<script>
export default {
  async fetch() {
    const tags = []

    const tagsPost = await this.$content('blog').only(['tags']).fetch()

    tagsPost.forEach(tagPost => {
      if(tags.indexOf(tagPost.tags) == -1){
        tags.push(tagPost.tags)
      }
    });

    this.tags = tags
  },
  data(){
    return {
      tags: [],
      open: false,
    }
  },
  // fetchOnServer: true
}
</script>

<style>

</style>
