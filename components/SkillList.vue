<template>
  <section class="skill-list w-100">
    <!-- Completed stats -->
    <div class="small muted">
      <!-- Filter and store in a array the items completed-->
      {{ content.globalCompleted[language] }}
      {{ skillItems.filter(skillItem => { return skillItem.skillCompleted === true }).length }}
      <!-- Filter and store in a array the items not completed-->
      {{ content.globalNotCompleted[language] }}
      {{ skillItems.filter(skillItem => { return skillItem.skillCompleted === false }).length }}
    </div>
    <SkillListItem
      v-for="(skillItem,index) in skillItems"
      :key="index"
      :skill-item="skillItem"
      :language="language"
      :content="content"
      @delete-item="deleteItem"
      @complete-item="completeItem"
      @incomplete-item="incompleteItem"
    />
  </section>
</template>

<script>
// Import
import SkillListItem from '@/components/SkillListItem.vue'
// Export
export default {
  // Name and components
  name: 'SkillList',
  components: {
    SkillListItem
  },
  // Properties received from parent
  props: ['skillItems', 'content', 'language'],
  methods: {
    // Delete items (the below methods can be in store)
    deleteItem (skillItem) {
      // Element index to be deleted
      const itemIndex = this.skillItems.indexOf(skillItem)
      // Method splice modify content of an arraylist, in this case remove 1 element of index itemIndex
      this.skillItems.splice(itemIndex, 1)
      // Update store via mutation (classic style)
      this.$store.commit('skill/set', this.skillItems)
    },
    // Completed items
    completeItem (skillItem) {
      // Select index
      const itemIndex = this.skillItems.indexOf(skillItem)
      // Set id of item
      skillItem.skillId = itemIndex
      // Modify state of item
      this.skillItems[itemIndex].skillCompleted = true
      // Update store via mutation (classic)
      this.$store.commit('skill/set', this.skillItems)
    },
    // Uncheck completed items
    incompleteItem (skillItem) {
      // Select element to be mark as completed
      const itemIndex = this.skillItems.indexOf(skillItem)
      // Modify state of item
      this.skillItems[itemIndex].skillCompleted = false
      // Update store via mutation (classic)
      this.$store.commit('skill/set', this.skillItems.filter((skillItem) => { return skillItem.skillCompleted === true }))
    }
  }
}
</script>

<style>
</style>
