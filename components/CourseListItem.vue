<template>
  <section class="course-list-item my-3 w-100">
    <!-- Show mode -->
    <b-card
      v-show="!isEditing"
      bg-variant="white"
      class="mx-lg-5 shadow"
    >
      <!-- Data presentation -->
      <b-card-body>
        <b-card-title>
          {{ courseItem.courseTitle }}
        </b-card-title>
        <b-card-sub-title class="mb-2">
          {{ courseItem.courseDuration }}
        </b-card-sub-title>
        <b-card-text>
          {{ courseItem.courseDescription }}
        </b-card-text>
      </b-card-body>
      <!-- Edit and delete buttons -->
      <div class="my-3">
        <!-- Edit -->
        <span class="pr-3">
          <b-icon
            icon="pencil-square"
            class="b-icon-up-simple"
            @click="showForm"
          />
        </span>
        <!-- Delete -->
        <span class="pl-3">
          <b-icon
            icon="dash-square"
            variant="danger"
            class="b-icon-up-simple"
            @click="deleteItem(courseItem)"
          />
        </span>
      </div>
      <!-- Complete and incomplete state toggle with toast and tooltip -->
      <div class="d-flex justify-content-end">
        <b-button
          id="tooltip-target-2"
          variant="outline-secondary"
        >
          <div class="d-flex justify-content-end">
            <!-- Label -->
            <span class="mr-3">
              {{ content.completedLabel[language] }}
            </span>
            <!-- Incomplete -->
            <div
              v-show="!isEditing && courseItem.courseCompleted"
              @click="incompleteItem(courseItem) ; incompletedToast()"
            >
              <b-icon icon="circle-fill" variant="success" />
            </div>
            <!-- Complete -->
            <div
              v-show="!isEditing && !courseItem.courseCompleted"
              @click="completeItem(courseItem) ; completedToast()"
            >
              <b-icon icon="circle-fill" variant="outline-danger" />
            </div>
          </div>
        </b-button>
        <!-- Tooltip -->
        <b-tooltip target="tooltip-target-2" placement="left" triggers="hover">
          {{ content.completedInfo[language] }}
        </b-tooltip>
      </div>
    </b-card>
    <!-- Edition mode -->
    <b-card
      v-show="isEditing"
      bg-variant="light"
      class="mx-lg-5 shadow"
    >
      <!-- Form -->
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
          label-for="courseTitle"
        >
          <b-form-input
            id="courseTitle"
            v-model="courseItem.courseTitle"
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
          label-for="courseDuration"
        >
          <b-form-input
            id="courseDuration"
            v-model="courseItem.courseDuration"
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
          label-for="courseDescription"
        >
          <b-form-textarea
            id="courseDescription"
            v-model="courseItem.courseDescription"
            :placeholder="content.courseDescriptionPlaceholder[language]"
            type="textarea"
            rows="3"
          />
        </b-form-group>
      </b-form-group>
      <!-- Confirm edition -->
      <div>
        <b-icon
          icon="check-square"
          variant="success"
          class="b-icon-trans"
          @click="hideForm"
        />
      </div>
    </b-card>
  </section>
</template>

<script>
// Export
export default {
  // Name and components
  name: 'CourseListItem',
  // Properties received from parent
  props: ['courseItem', 'content', 'language'],
  data () {
    return {
      // Default items
      isEditing: false
    }
  },
  computed: {
    // Validation
    courseTitleState () {
      return this.courseItem.courseTitle.length > 5
    },
    courseDurationState () {
      return this.courseItem.courseDuration.length > 2
    },
    courseDescriptionState () {
      return this.courseItem.courseDescription.length > 3
    },
    courseTitleInvalid () {
      if (this.courseItem.courseTitle.length > 0) {
        return this.content.courseTitleInvalidVoid[this.language]
      }
      return this.content.courseTitleInvalid[this.language]
    },
    courseDurationInvalid () {
      if (this.courseItem.courseDuration.length > 0) {
        return this.content.courseDurationInvalidVoid[this.language]
      }
      return this.content.courseDurationInvalid[this.language]
    },
    courseDescriptionInvalid () {
      if (this.courseItem.courseDescription.length > 0) {
        return this.content.courseDescriptionInvalidVoid[this.language]
      }
      return this.content.courseDescriptionInvalid[this.language]
    }
  },
  methods: {
    // Methods for actions
    showForm () {
      this.isEditing = true
    },
    hideForm () {
      this.isEditing = false
    },
    // Toasts
    completedToast () {
      this.$bvToast.toast(this.content.completedMessageB[this.language], {
        title: this.content.completedMessageA[this.language],
        variant: 'success',
        solid: true
      })
    },
    incompletedToast () {
      this.$bvToast.toast(this.content.incompletedMessageB[this.language], {
        title: this.content.incompletedMessageA[this.language],
        variant: 'danger',
        solid: true
      })
    },
    // Pass to a parent method
    deleteItem (courseItem) {
      this.$emit('delete-item', courseItem)
    },
    completeItem (courseItem) {
      this.$emit('complete-item', courseItem)
    },
    incompleteItem (courseItem) {
      this.$emit('incomplete-item', courseItem)
    }
  }
}
</script>

<style scoped >
  .b-icon {
    font-size:1.5rem
  }
</style>
