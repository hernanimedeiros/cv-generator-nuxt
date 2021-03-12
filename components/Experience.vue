<template>
  <section class="experience my-5 w-100">
    <!-- Label -->
    <b-card
      :title="content.experienceCardTitle[language]"
      :sub-title="content.experienceCardSubTitle[language]"
      bg-variant="light"
      class="mx-lg-5 shadow"
    >
      <!-- List items -->
      <ExperienceList
        :experience-items="experienceItems"
        :language="language"
        :content="content"
      />
      <!-- Create items -->
      <ExperienceCreate
        :language="language"
        :content="content"
        @create-experience-item="createExperienceItem"
      />
    </b-card>
  </section>
</template>

<script>
// Import
import ExperienceList from '@/components/ExperienceList.vue'
import ExperienceCreate from '@/components/ExperienceCreate.vue'
// Export
export default {
  // Name and components
  name: 'Experience',
  components: {
    ExperienceList,
    ExperienceCreate
  },
  // Parameters received by parent
  props: ['content', 'language'],
  data () {
    return {
      // Default items
      experienceItems: [
        {
          experienceId: 0,
          experienceTitle: this.content.experienceTitlePlaceholder[this.language],
          experienceSubTitle: this.content.experienceSubTitlePlaceholder[this.language],
          experienceDuration: this.content.experienceDurationPlaceholder[this.language],
          experienceDescription: this.content.experienceDescriptionPlaceholder[this.language],
          experienceCompleted: false
        }
      ]
    }
  },
  methods: {
    // Append item
    createExperienceItem (experienceItem) {
      this.experienceItems.push(experienceItem)
    }
  }
}
</script>

<style>
</style>
