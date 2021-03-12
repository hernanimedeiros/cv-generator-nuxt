<template>
  <section class="skill my-5 w-100">
    <b-card
      :title="content.skillCardTitle[language]"
      :sub-title="content.skillCardSubTitle[language]"
      bg-variant="light"
      class="mx-lg-5 shadow"
    >
      <!-- List items -->
      <SkillList
        :skill-items="skillItems"
        :language="language"
        :content="content"
      />
      <!-- Create items -->
      <SkillCreate
        :language="language"
        :content="content"
        @create-skill-item="createSkillItem"
      />
    </b-card>
  </section>
</template>

<script>
// Import
import SkillList from '@/components/SkillList.vue'
import SkillCreate from '@/components/SkillCreate.vue'
// Export
export default {
  // Name and components
  name: 'Skill',
  components: {
    SkillList,
    SkillCreate
  },
  // Parameters received by parent
  props: ['content', 'language'],
  data () {
    return {
      // Default items
      skillItems: [
        {
          skillId: 0,
          skillTitle: this.content.skillTitlePlaceholder[this.language],
          skillRating: 5,
          skillDescription: this.content.skillDescriptionPlaceholder[this.language],
          skillCompleted: false
        }
      ]
    }
  },
  methods: {
    // Append item
    createSkillItem (skillItem) {
      this.skillItems.push(skillItem)
    }
  }
}
</script>

<style>
</style>
