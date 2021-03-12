<template>
  <section class="education-list w-100">
    <!-- Completed stats -->
    <div class="small muted">
      <!-- Filter and store in a array the items completed-->
      {{ content.globalCompleted[language] }}
      {{ educationItems.filter(educationItem => { return educationItem.educationCompleted === true }).length }}
      <!-- Filter and store in a array the items not completed-->
      {{ content.globalNotCompleted[language] }}
      {{ educationItems.filter(educationItem => { return educationItem.educationCompleted === false }).length }}
    </div>
    <EducationListItem
      v-for="(educationItem,index) in educationItems"
      :key="index"
      :education-item="educationItem"
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
import EducationListItem from '@/components/EducationListItem.vue'
import { mapMutations } from 'vuex'
// Export
export default {
  // Name and components
  name: 'EducationList',
  components: {
    EducationListItem
  },
  // Properties received from parent
  props: ['educationItems', 'content', 'language'],
  methods: {
    // Shortcut to mutations
    ...mapMutations({
      change: 'education/set'
    }),
    // Delete items (the below methods can be in store)
    deleteItem (educationItem) {
      // Element index to be deleted
      const itemIndex = this.educationItems.indexOf(educationItem)
      // Method splice modify content of an arraylist, in this case remove 1 element of index itemIndex
      this.educationItems.splice(itemIndex, 1)
      // Update store via mutation
      this.change(this.educationItems)
    },
    // Completed items
    completeItem (educationItem) {
      // Select index
      const itemIndex = this.educationItems.indexOf(educationItem)
      // Set id of item
      educationItem.educationId = itemIndex
      // Modify state of item
      this.educationItems[itemIndex].educationCompleted = true
      // Update store via mutation
      this.change(this.educationItems)
    },
    // Uncheck completed items
    incompleteItem (educationItem) {
      // Select element to be mark as completed
      const itemIndex = this.educationItems.indexOf(educationItem)
      // Modify state of item
      this.educationItems[itemIndex].educationCompleted = false
      // Update store via mutation
      this.change(this.educationItems.filter((educationItem) => { return educationItem.educationCompleted === true }))
    }
  }
}
</script>

<style>
</style>
