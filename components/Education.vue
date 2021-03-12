<template>
  <section class="education my-5 w-100">
    <!-- Label -->
    <b-card
      :title="content.educationCardTitle[language]"
      :sub-title="content.educationCardSubTitle[language]"
      bg-variant="light"
      class="mx-lg-5 shadow"
    >
      <!-- List items -->
      <EducationList
        :education-items="educationItems"
        :language="language"
        :content="content"
      />
      <!-- Create items -->
      <EducationCreate
        :language="language"
        :content="content"
        @create-education-item="createEducationItem"
      />
    </b-card>
  </section>
</template>

<script>
// Import
import EducationList from '@/components/EducationList.vue'
import EducationCreate from '@/components/EducationCreate.vue'
// Export
export default {
  // Name and components
  name: 'Education',
  components: {
    EducationList,
    EducationCreate
  },
  // Parameters received by parent
  props: ['content', 'language'],
  data () {
    return {
      // Default items
      educationItems: [
        {
          educationId: 0,
          educationTitle: this.content.educationTitlePlaceholder[this.language],
          educationDuration: this.content.educationDurationPlaceholder[this.language],
          educationDescription: this.content.educationDescriptionPlaceholder[this.language],
          educationCompleted: false
        }
      ]
    }
  },
  methods: {
    // Append item
    createEducationItem (educationItem) {
      this.educationItems.push(educationItem)
    }
  }
}
</script>

<style>
</style>
