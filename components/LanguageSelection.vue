<template>
  <section class="language-set-selection w-100">
    <b-container fluid>
      <b-row>
        <!-- Language change -->
        <b-col cols="11">
          <b-form-select
            v-model="selected"
            :options="options"
            value-field="item"
            text-field="name"
            disabled-field="notEnabled"
            class="pr-1"
            @change="flagLink;flagAlt;changeLanguage(selected)"
          />
        </b-col>
        <!-- Display flag -->
        <b-col cols="1">
          <b-img
            :src="flagLink()"
            :alt="flagAlt()"
            class="flag-icon pl-1"
          />
        </b-col>
      </b-row>
    </b-container>
  </section>
</template>

<script>
// Export
export default {
  name: 'LanguageSelection',
  props: ['content', 'language', 'preferences'],
  data () {
    return {
      // Default value on form
      selected: this.preferences[0].language,
      // Language available
      options: [
        { item: 'pt', name: 'Português' },
        { item: 'en', name: 'English' }
      ]
    }
  },
  methods: {
    // Dinamic change src path
    flagLink () {
      const lang = this.selected
      return require('@/assets/' + lang + '.svg')
    },
    // Dinamic change of alt attribute
    flagAlt () {
      return this.content.flagName[this.selected]
    },
    // Change language
    changeLanguage (language) {
      this.preferences[0].language = language
    }
  }
}
</script>

<style scoped >
  .flag-icon {
    width: 2rem;
  }
</style>
