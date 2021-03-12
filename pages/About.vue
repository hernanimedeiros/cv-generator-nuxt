<template>
  <section class="about w-100">
    <AboutPage
      :language="checkLanguage"
      :content="content"
    />
  </section>
</template>

<script>
// Import
// @ is an alias to /src
import { mapGetters } from 'vuex'
import ContentJson from '@/content.json'
import AboutPage from '@/components/AboutPage.vue'
// Export
export default {
  // Name and components
  name: 'About',
  components: {
    AboutPage
  },
  layout (context) {
    return 'about'
  },
  data () {
    return {
      content: ContentJson
    }
  },
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
      title: this.content.metaAboutTitle[this.checkLanguage],
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: this.content.metaAboutDescription[this.checkLanguage]
        },
        {
          hid: 'keywords',
          name: 'keywords',
          content: this.content.metaAboutKeyword[this.checkLanguage]
        }
      ],
      script: [
        {
          src: 'https://kit.fontawesome.com/34ea097e0f.js',
          crossorigin: 'anonymous'
        }
      ]
    }
  }
}
</script>

<style>
</style>
