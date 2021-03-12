<template>
  <section class="education-list-item my-3 w-100">
    <!-- Show mode -->
    <b-card
      v-show="!isEditing"
      bg-variant="white"
      class="mx-lg-5 shadow"
    >
      <!-- Data presentation -->
      <b-card-body>
        <b-card-title>
          {{ educationItem.educationTitle }}
        </b-card-title>
        <b-card-sub-title class="mb-2">
          {{ educationItem.educationDuration }}
        </b-card-sub-title>
        <b-card-text>
          {{ educationItem.educationDescription }}
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
            @click="deleteItem(educationItem)"
          />
        </span>
      </div>
      <!-- Complete and incomplete state toggle -->
      <div class="d-flex justify-content-end">
        <b-button
          id="tooltip-target-3"
          variant="outline-secondary"
        >
          <div class="d-flex justify-content-end">
            <!-- Label -->
            <span class="mr-3">
              {{ content.completedLabel[language] }}
            </span>
            <!-- Incomplete -->
            <div
              v-show="!isEditing && educationItem.educationCompleted"
              @click="incompleteItem(educationItem) ; incompletedToast()"
            >
              <b-icon
                icon="circle-fill"
                variant="success"
              />
            </div>
            <!-- Complete -->
            <div
              v-show="!isEditing && !educationItem.educationCompleted"
              @click="completeItem(educationItem) ; completedToast()"
            >
              <b-icon
                icon="circle-fill"
                variant="outline-danger"
              />
            </div>
          </div>
        </b-button>
        <!-- Tooltip -->
        <b-tooltip target="tooltip-target-3" placement="left" triggers="hover">
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
        :label="content.educationLabel[language]"
        label-cols-lg="3"
        label-size="lg"
        label-class="font-weight-bold pt-0"
        class="mb-0"
      >
        <!-- Item -->
        <b-form-group
          :label="content.educationTitle[language]"
          :valid-feedback="content.globalThanksA[language]"
          :invalid-feedback="educationTitleInvalid"
          :state="educationTitleState"
          label-cols-sm="3"
          label-align-sm="right"
          label-for="educationTitle"
        >
          <b-form-input
            id="educationTitle"
            v-model="educationItem.educationTitle"
            :placeholder="content.educationTitlePlaceholder[language]"
            type="text"
          />
        </b-form-group>
        <!-- Item -->
        <b-form-group
          :label="content.educationDuration[language]"
          :valid-feedback="content.globalThanksB[language]"
          :invalid-feedback="educationDurationInvalid"
          :state="educationDurationState"
          label-cols-sm="3"
          label-align-sm="right"
          label-for="educationDuration"
        >
          <b-form-input
            id="educationDuration"
            v-model="educationItem.educationDuration"
            :placeholder="content.educationDurationPlaceholder[language]"
            type="text"
          />
        </b-form-group>
        <!-- Item -->
        <b-form-group
          :label="content.educationDescription[language]"
          :valid-feedback="content.globalThanksC[language]"
          :invalid-feedback="educationDescriptionInvalid"
          :state="educationDescriptionState"
          label-cols-sm="3"
          label-align-sm="right"
          label-for="educationDescription"
        >
          <b-form-textarea
            id="educationDescription"
            v-model="educationItem.educationDescription"
            :placeholder="content.educationDescriptionPlaceholder[language]"
            type="text"
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
  name: 'EducationListItem',
  // Properties received from parent
  props: ['educationItem', 'content', 'language'],
  data () {
    return {
      // Default items
      isEditing: false
    }
  },
  computed: {
    // Validation
    educationTitleState () {
      return this.educationItem.educationTitle.length > 5
    },
    educationDurationState () {
      return this.educationItem.educationDuration.length > 4
    },
    educationDescriptionState () {
      return this.educationItem.educationDescription.length > 3
    },
    educationTitleInvalid () {
      if (this.educationItem.educationTitle.length > 0) {
        return this.content.educationTitleInvalidVoid[this.language]
      }
      return this.content.educationTitleInvalid[this.language]
    },
    educationDurationInvalid () {
      if (this.educationItem.educationDuration.length > 0) {
        return this.content.educationDurationInvalidVoid[this.language]
      }
      return this.content.educationDurationInvalid[this.language]
    },
    educationDescriptionInvalid () {
      if (this.educationItem.educationDescription.length > 0) {
        return this.content.educationDescriptionInvalidVoid[this.language]
      }
      return this.content.educationDescriptionInvalid[this.language]
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
    deleteItem (educationItem) {
      this.$emit('delete-item', educationItem)
    },
    completeItem (educationItem) {
      this.$emit('complete-item', educationItem)
    },
    incompleteItem (educationItem) {
      this.$emit('incomplete-item', educationItem)
    }
  }
}
</script>

<style scoped >
  .b-icon {
    font-size:1.5rem
  }
</style>
