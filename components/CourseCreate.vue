<template>
  <section class="course-create my-3 w-100">
    <!-- Create OFF. Can call create mode -->
    <span class="shadow">
      <b-icon
        v-show="!isCreating"
        icon="plus-square-fill"
        variant="success"
        class="b-icon-trans"
        @click="openForm"
      />
    </span>
    <!-- Create ON. card->form-group->form-input... -->
    <b-card
      v-show="isCreating"
      bg-variant="white"
      class="mx-lg-5 shadow"
    >
      <!-- Label -->
      <b-form-group
        :label="content.courseLabel[language]"
        label-cols-lg="3"
        label-size="lg"
        label-class="font-weight-bold pt-0"
        class="mb-0"
      >
        <!-- Item -->
        <b-form-group
          :label="content.courseTitle[language]"
          :valid-feedback="content.globalThanksA[language]"
          :invalid-feedback="courseTitleInvalid"
          :state="courseTitleState"
          label-cols-sm="3"
          label-align-sm="right"
          label-for="courseTitleCreate"
        >
          <b-form-input
            id="courseTitleCreate"
            v-model="courseTitle"
            :placeholder="content.courseTitlePlaceholder[language]"
            type="text"
          />
        </b-form-group>
        <!-- Item -->
        <b-form-group
          :label="content.courseDuration[language]"
          :valid-feedback="content.globalThanksB[language]"
          :invalid-feedback="courseDurationInvalid"
          :state="courseDurationState"
          label-cols-sm="3"
          label-align-sm="right"
          label-for="courseDurationCreate"
        >
          <b-form-input
            id="courseDurationCreate"
            v-model="courseDuration"
            :placeholder="content.courseDurationPlaceholder[language]"
            type="text"
          />
        </b-form-group>
        <!-- Item -->
        <b-form-group
          :label="content.courseDescription[language]"
          :valid-feedback="content.globalThanksC[language]"
          :invalid-feedback="courseDescriptionInvalid"
          :state="courseDescriptionState"
          label-cols-sm="3"
          label-align-sm="right"
          label-for="courseDescriptionCreate"
        >
          <b-form-textarea
            id="courseDescriptionCreate"
            v-model="courseDescription"
            :placeholder="content.courseDescriptionPlaceholder[language]"
            type="textarea"
            rows="3"
          />
        </b-form-group>
      </b-form-group>
      <!-- Confirm or cancel changes -->
      <div class="d-flex justify-content-end">
        <span
          class="pr-3"
          @click="sendForm"
        >
          <b-icon
            icon="hand-thumbs-up"
            variant="success"
            class="b-icon-up"
          />
        </span>
        <span
          class="pl-3"
          @click="closeForm"
        >
          <b-icon
            icon="hand-thumbs-down"
            variant="danger"
            class="b-icon-up"
          />
        </span>
      </div>
    </b-card>
  </section>
</template>

<script>
// Export
export default {
  // Name and components
  name: 'CourseCreate',
  // Parameters received by parent
  props: ['content', 'language'],
  data () {
    // Default items
    return {
      courseId: '',
      courseTitle: '',
      courseDuration: '',
      courseDescription: '',
      isCreating: false
    }
  },
  computed: {
    // Validation
    courseTitleState () {
      return this.courseTitle.length > 5
    },
    courseDurationState () {
      return this.courseDuration.length > 4
    },
    courseDescriptionState () {
      return this.courseDescription.length > 3
    },
    courseTitleInvalid () {
      if (this.courseTitle.length > 0) {
        return this.content.courseTitleInvalidVoid[this.language]
      }
      return this.content.courseTitleInvalid[this.language]
    },
    courseDurationInvalid () {
      if (this.courseDuration.length > 0) {
        return this.content.courseDurationInvalidVoid[this.language]
      }
      return this.content.courseDurationInvalid[this.language]
    },
    courseDescriptionInvalid () {
      if (this.courseDescription.length > 0) {
        return this.content.courseDescriptionInvalidVoid[this.language]
      }
      return this.content.courseDescriptionInvalid[this.language]
    }
  },
  // Methods for actions
  methods: {
    openForm () {
      this.isCreating = true
    },
    closeForm () {
      this.isCreating = false
    },
    sendForm () {
      // Check data inserted if conditions are accomplished
      if (this.courseTitle.length > 5 && this.courseDuration.length > 4 && this.courseDescription.length > 3) {
        const courseId = this.courseId
        const courseTitle = this.courseTitle
        const courseDuration = this.courseDuration
        const courseDescription = this.courseDescription
        // Pass to a parent method
        this.$emit('create-course-item', {
          courseId,
          courseTitle,
          courseDuration,
          courseDescription,
          courseCompleted: false
        })
        // Reset after emit
        this.courseId = ''
        this.courseTitle = ''
        this.courseDuration = ''
        this.courseDescription = ''
        this.isCreating = false
      }
    }
  }
}
</script>

<style scoped >
  .b-icon {
    font-size:1.5rem
  }
</style>
