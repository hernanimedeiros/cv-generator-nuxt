<template>
  <section class="homepage w-100">
    <Home :language="checkLanguage" :content="content" />
  </section>
</template>

<script>
// Import
// @ is an alias to /src
import { mapGetters } from 'vuex'
import ContentJson from '@/content.json'
import Home from '@/components/Home.vue'
// Export
export default {
  // Name and components
  name: 'Index',
  components: {
    Home
  },
  data () {
    return {
      content: ContentJson
    }
  },
  // Watch store
  computed: {
    ...mapGetters({
      getPreferences: 'preferences/get'
    }),
    checkLanguage () {
      // Check current language, force 'pt' if dont come of index
      try {
        const currentLanguage = this.getPreferences[0].language
        return currentLanguage
      } catch (e) {
        return 'pt'
      }
    }
  },
  head () {
    return {
      htmlAttrs: {
        lang: this.checkLanguage
      },
      title: this.content.metaHomeTitle[this.checkLanguage],
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: this.content.metaHomeDescription[this.checkLanguage]
        },
        {
          hid: 'keywords',
          name: 'keywords',
          content: this.content.metaHomeKeyword[this.checkLanguage]
        }
      ]
    }
  }
}
</script>

<style>

</style>
