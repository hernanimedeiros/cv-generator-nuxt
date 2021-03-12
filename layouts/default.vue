<template>
  <!-- This component control main store -->
  <section class="default-layout w-100">
    <!-- Navbar with language set -->
    <DinamicNav
      :content="content"
      :language="checkLanguage"
      :preferences="preferences"
    />
    <!-- Main -->
    <Nuxt />
    <!-- Footer -->
    <DinamicFooter
      :content="content"
      :language="checkLanguage"
    />
  </section>
</template>

<script>
// Import
// @ is an alias to /src
import ContentJson from '@/content.json'
import { mapGetters, mapState, mapMutations } from 'vuex'
import DinamicNav from '@/components/DinamicNav.vue'
import DinamicFooter from '@/components/DinamicFooter.vue'
// Export
export default {
  // Name and components
  name: 'DefaultLayout',
  components: {
    DinamicNav,
    DinamicFooter
  },
  // To use in future versions
  // fetch(context) is called by the server-side
  // and before instantiating the component
  fetch ({ store }) {
    store.commit('increment')
  },
  data () {
    return {
      // Load content
      content: ContentJson,
      // Default app settings
      preferences: [
        {
          language: 'pt',
          // In development
          colorMode: 'light'
        }
      ]
    }
  },
  computed: {
    ...mapState({
      counter: 'counter'
    }),
    ...mapGetters({
      getPreferences: 'preferences/get'
    }),
    checkLanguage () {
      // Check current language, force default one if dont come of index
      try {
        const currentLanguage = this.getPreferences[0].language
        return currentLanguage
      } catch (e) {
        return this.preferences[0].language
      }
    }
  },
  mounted () {
    // Can choose classic store commit or with Map implementation
    // this.$store.commit('preferences/set', this.preferences)
    this.setPreferences(this.preferences)
  },
  methods: {
    ...mapMutations({
      setPreferences: 'preferences/set'
    }),
    increment () {
      this.$store.commit('increment')
    }
  }
}
</script>

<style>
  html {
    font-family:
      Roboto,
      -apple-system,
      'Helvetica Neue',
      BlinkMacSystemFont,
      'Segoe UI',
      Arial,
      sans-serif;
    font-size: 16px;
    word-spacing: 1px;
    -ms-text-size-adjust: 100%;
    -webkit-text-size-adjust: 100%;
    -moz-osx-font-smoothing: grayscale;
    -webkit-font-smoothing: antialiased;
    text-align: center;
    overflow-x: hidden;
    box-sizing: border-box;
    margin: 0;
    padding: 0;
    outline: 0;
    scroll-behavior: smooth;
  }

  *,

  *::before,

  *::after {
    box-sizing: border-box;
    margin: 0;
    text-align: center;
  }

  .b-icon-trans {
    filter: grayscale(100%);
    transition-delay: 0.25s;
    transition-timing-function: ease-out;
    transition: transform 0.4s, filter 1s;
  }

  .b-icon-trans:hover {
    transform: scale(1.5);
    filter: grayscale(0%);
  }

  .b-icon-up {
    filter: grayscale(100%);
    transition-delay: 0.25s;
    transition-timing-function: ease-out;
    transition: transform 0.4s, filter 1s;
  }

  .b-icon-up:hover {
    transform: translateY(-5%);
    filter: grayscale(0%);
  }

  .b-icon-up-simple {
    transition-delay: 0.25s;
    transition-timing-function: ease-in-out;
    transition: transform 0.5s;
  }

  .b-icon-up-simple:hover {
    transform: translateY(-5%);
  }
</style>
