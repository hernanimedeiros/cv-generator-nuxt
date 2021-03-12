<template>
  <section class="course-list w-100">
    <!-- Completed stats -->
    <div class="small muted">
      <!-- Filter and store in a array the items completed-->
      {{ content.globalCompleted[language] }}
      {{ courseItems.filter(courseItem => { return courseItem.courseCompleted === true }).length }}
      <!-- Filter and store in a array the items not completed-->
      {{ content.globalNotCompleted[language] }}
      {{ courseItems.filter(courseItem => { return courseItem.courseCompleted === false }).length }}
    </div>
    <CourseListItem
      v-for="(courseItem,index) in courseItems"
      :key="index"
      :course-item="courseItem"
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
import CourseListItem from '@/components/CourseListItem.vue'
import { mapMutations } from 'vuex'
// Export
export default {
  // Name and components
  name: 'CourseList',
  components: {
    CourseListItem
  },
  // Properties received from parent
  props: ['courseItems', 'content', 'language'],
  methods: {
    // Shortcut to mutations
    ...mapMutations({
      change: 'course/set'
    }),
    // Delete items (the below methods can be in store)
    deleteItem (courseItem) {
      // Element index to be deleted
      const itemIndex = this.courseItems.indexOf(courseItem)
      // Method splice modify content of an arraylist, in this case remove 1 element of index itemIndex
      this.courseItems.splice(itemIndex, 1)
      // Update store via mutation
      this.change(this.courseItems)
    },
    // Completed items
    completeItem (courseItem) {
      // Select index
      const itemIndex = this.courseItems.indexOf(courseItem)
      // Set id of item
      courseItem.courseId = itemIndex
      // Modify state of item
      this.courseItems[itemIndex].courseCompleted = true
      // Update store via mutation
      this.change(this.courseItems)
    },
    // Uncheck completed items
    incompleteItem (courseItem) {
      // Select element to be mark as completed
      const itemIndex = this.courseItems.indexOf(courseItem)
      // Modify state of item
      this.courseItems[itemIndex].courseCompleted = false
      // Update store via mutation
      this.change(this.courseItems.filter((courseItem) => { return courseItem.courseCompleted === true }))
    }
  }
}
</script>

<style>
</style>
