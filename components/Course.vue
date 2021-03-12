<template>
  <section class="course my-5 w-100">
    <!-- Label -->
    <b-card
      :title="content.courseCardTitle[language]"
      :sub-title="content.courseCardSubTitle[language]"
      bg-variant="light"
      class="mx-lg-5 shadow"
    >
      <!-- List items -->
      <CourseList
        :course-items="courseItems"
        :language="language"
        :content="content"
      />
      <!-- Create items -->
      <CourseCreate
        :language="language"
        :content="content"
        @create-course-item="createCourseItem"
      />
    </b-card>
  </section>
</template>

<script>
// Import
import CourseList from '@/components/CourseList.vue'
import CourseCreate from '@/components/CourseCreate.vue'
// Export
export default {
  // Name and components
  name: 'Course',
  components: {
    CourseList,
    CourseCreate
  },
  // Parameters received by parent
  props: ['content', 'language'],
  data () {
    return {
      // Default items
      courseItems: [
        {
          courseId: 0,
          courseTitle: this.content.courseTitlePlaceholder[this.language],
          courseDuration: this.content.courseDurationPlaceholder[this.language],
          courseDescription: this.content.courseDescriptionPlaceholder[this.language],
          courseCompleted: false
        }
      ]
    }
  },
  methods: {
    // Append item
    createCourseItem (courseItem) {
      this.courseItems.push(courseItem)
    }
  }
}
</script>

<style>
</style>
