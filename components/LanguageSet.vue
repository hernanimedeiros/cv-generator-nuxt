<template>
  <section class="language-set w-100">
    <!-- Icon to activate modal -->
    <span>
      <b-icon
        icon="globe2"
        @click="$bvModal.show('bv-modal-language')"
      />
    </span>
    <!-- Modal to change language -->
    <b-modal id="bv-modal-language" hide-footer>
      <template #modal-title>
        {{ content.languageTitle[language] }}
      </template>
      <div class="d-block text-center">
        <!-- Language change component -->
        <LanguageSelection
          :content="content"
          :language="language"
          :preferences="preferences"
        />
      </div>
      <b-button
        class="mt-3"
        block
        @click="$bvModal.hide('bv-modal-language')"
      >
        {{ content.languageSelection[language] }}
      </b-button>
    </b-modal>
  </section>
</template>

<script>
import LanguageSelection from '@/components/LanguageSelection.vue'
export default {
  // Name and components
  name: 'LanguageSet',
  components: {
    LanguageSelection
  },
  // Properties received from parent
  props: ['content', 'language', 'preferences'],
  data () {
    return {
      // Show modal on mount of component dont need do declare
      modalLangShow: false
    }
  }
  /* mounted () {
    Modal delay trigger
    setTimeout(this.modalDelay, 1000)
  },
  methods: {
    // Modal delay
    modalDelay () {
      this.$bvModal.show('bv-modal-language')
    }
  } */
}
</script>

<style scoped>
  .b-icon {
    color: whitesmoke;
  }

  .b-icon:hover {
    color: lightgrey;
  }
</style>
