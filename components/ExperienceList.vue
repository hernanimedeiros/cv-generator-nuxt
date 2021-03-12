<template>
  <section class="experience-list w-100">
    <!-- Completed stats -->
    <div class="small muted">
      <!-- Filter and store in a array the items completed-->
      {{ content.globalCompleted[language] }}
      {{ experienceItems.filter(experienceItem => { return experienceItem.experienceCompleted === true }).length }}
      <!-- Filter and store in a array the items not completed-->
      {{ content.globalNotCompleted[language] }}
      {{ experienceItems.filter(experienceItem => { return experienceItem.experienceCompleted === false }).length }}
    </div>
    <ExperienceListItem
      v-for="(experienceItem,index) in experienceItems"
      :key="index"
      :experience-item="experienceItem"
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
import ExperienceListItem from '@/components/ExperienceListItem.vue'
import { mapMutations } from 'vuex'
// Export
export default {
  // Name and components
  name: 'ExperienceList',
  components: {
    ExperienceListItem
  },
  // Properties received from parent
  props: ['experienceItems', 'content', 'language'],
  methods: {
    // Shortcut to mutations
    ...mapMutations({
      change: 'experience/set'
    }),
    // Delete items (the below methods can be in store)
    deleteItem (experienceItem) {
      // Element index to be deleted
      const itemIndex = this.experienceItems.indexOf(experienceItem)
      // Method splice modify content of an arraylist, in this case remove 1 element of index itemIndex
      this.experienceItems.splice(itemIndex, 1)
      // Update store via mutation
      this.change(this.experienceItems)
    },
    // Completed items
    completeItem (experienceItem) {
      // Select index
      const itemIndex = this.experienceItems.indexOf(experienceItem)
      // Set id of item
      experienceItem.experienceId = itemIndex
      // Modify state of item
      this.experienceItems[itemIndex].experienceCompleted = true
      // Update store via mutation
      this.change(this.experienceItems)
    },
    // Uncheck completed items
    incompleteItem (experienceItem) {
      // Select element to be mark as completed
      const itemIndex = this.experienceItems.indexOf(experienceItem)
      // Modify state of item
      this.experienceItems[itemIndex].experienceCompleted = false
      // Update store via mutation
      this.change(this.experienceItems.filter((experienceItem) => { return experienceItem.experienceCompleted === true }))
    }
  }
}
</script>

<style>
</style>
