<template>
  <section class="experience-list-item my-3 w-100">
    <!-- Show mode -->
    <b-card
      v-show="!isEditing"
      bg-variant="white"
      class="mx-lg-5 shadow"
    >
      <!-- Data presentation -->
      <b-card-body>
        <b-card-title>
          {{ experienceItem.experienceTitle }}
        </b-card-title>
        <b-card-sub-title class="mb-2">
          {{ experienceItem.experienceSubTitle }}
        </b-card-sub-title>
        <b-card-sub-title class="mb-2">
          {{ experienceItem.experienceDuration }}
        </b-card-sub-title>
        <b-card-text>
          {{ experienceItem.experienceDescription }}
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
            @click="deleteItem(experienceItem)"
          />
        </span>
      </div>
      <!-- Complete and incomplete state toggle -->
      <div class="d-flex justify-content-end">
        <b-button
          id="tooltip-target-4"
          variant="outline-secondary"
        >
          <div class="d-flex justify-content-end">
            <!-- Label -->
            <span class="mr-3">
              {{ content.completedLabel[language] }}
            </span>
            <!-- Incomplete -->
            <div
              v-show="!isEditing && experienceItem.experienceCompleted"
              @click="incompleteItem(experienceItem) ; incompletedToast()"
            >
              <b-icon
                icon="circle-fill"
                variant="success"
              />
            </div>
            <!-- Complete -->
            <div
              v-show="!isEditing && !experienceItem.experienceCompleted"
              @click="completeItem(experienceItem) ; completedToast()"
            >
              <b-icon
                icon="circle-fill"
                variant="outline-danger"
              />
            </div>
          </div>
        </b-button>
        <!-- Tooltip -->
        <b-tooltip target="tooltip-target-4" placement="left" triggers="hover">
          {{ content.completedInfo[language] }}
        </b-tooltip>
      </div>
    </b-card>

    <!-- Edition mode -->
    <b-card v-show="isEditing" bg-variant="light" class="mx-lg-5 shadow">
      <!-- Form -->
      <b-form-group
        :label="content.experienceLabel[language]"
        label-cols-lg="3"
        label-size="lg"
        label-class="font-weight-bold pt-0"
        class="mb-0"
      >
        <!-- Item -->
        <b-form-group
          :label="content.experienceTitle[language]"
          :valid-feedback="content.globalThanksA[language]"
          :invalid-feedback="experienceTitleInvalid"
          :state="experienceTitleState"
          label-cols-sm="3"
          label-align-sm="right"
          label-for="experienceTitle"
        >
          <b-form-input
            id="experienceTitle"
            v-model="experienceItem.experienceTitle"
            :placeholder="content.experienceTitlePlaceholder[language]"
            type="text"
          />
        </b-form-group>
        <!-- Item -->
        <b-form-group
          :label="content.experienceSubTitle[language]"
          :valid-feedback="content.globalThanksA[language]"
          :invalid-feedback="experienceSubTitleInvalid"
          :state="experienceSubTitleState"
          label-cols-sm="3"
          label-align-sm="right"
          label-for="experienceSubTitle"
        >
          <b-form-input
            id="experienceSubTitle"
            v-model="experienceItem.experienceSubTitle"
            :placeholder="content.experienceSubTitlePlaceholder[language]"
            type="text"
          />
        </b-form-group>
        <!-- Item -->
        <b-form-group
          :label="content.experienceDuration[language]"
          :valid-feedback="content.globalThanksB[language]"
          :invalid-feedback="experienceDurationInvalid"
          :state="experienceDurationState"
          label-cols-sm="3"
          label-align-sm="right"
          label-for="experienceDuration"
        >
          <b-form-input
            id="experienceDuration"
            v-model="experienceItem.experienceDuration"
            :placeholder="content.experienceDurationPlaceholder[language]"
            type="text"
          />
        </b-form-group>
        <!-- Item -->
        <b-form-group
          :label="content.experienceDescription[language]"
          :valid-feedback="content.globalThanksC[language]"
          :invalid-feedback="experienceDescriptionInvalid"
          :state="experienceDescriptionState"
          label-cols-sm="3"
          label-align-sm="right"
          label-for="experienceDescription"
        >
          <b-form-textarea
            id="experienceDescription"
            v-model="experienceItem.experienceDescription"
            :placeholder="content.experienceDescriptionPlaceholder[language]"
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
  name: 'ExperienceListItem',
  // Properties received from parent
  props: ['experienceItem', 'content', 'language'],
  data () {
    return {
      // Default items
      isEditing: false
    }
  },
  computed: {
    // Validation
    experienceTitleState () {
      return this.experienceItem.experienceTitle.length > 5
    },
    experienceSubTitleState () {
      return this.experienceItem.experienceTitle.length > 5
    },
    experienceDurationState () {
      return this.experienceItem.experienceDuration.length > 4
    },
    experienceDescriptionState () {
      return this.experienceItem.experienceDescription.length > 3
    },
    experienceTitleInvalid () {
      if (this.experienceItem.experienceTitle.length > 0) {
        return this.content.experienceTitleInvalidVoid[this.language]
      }
      return this.content.experienceTitleInvalid[this.language]
    },
    experienceSubTitleInvalid () {
      if (this.experienceItem.experienceTitle.length > 0) {
        return this.content.experienceTitleInvalidVoid[this.language]
      }
      return this.content.experienceTitleInvalid[this.language]
    },
    experienceDurationInvalid () {
      if (this.experienceItem.experienceDuration.length > 0) {
        return this.content.experienceDurationInvalidVoid[this.language]
      }
      return this.content.experienceDurationInvalid[this.language]
    },
    experienceDescriptionInvalid () {
      if (this.experienceItem.experienceDescription.length > 0) {
        return this.content.experienceDescriptionInvalidVoid[this.language]
      }
      return this.content.experienceDescriptionInvalid[this.language]
    }
  },
  // Methods for actions
  methods: {
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
    deleteItem (experienceItem) {
      this.$emit('delete-item', experienceItem)
    },
    completeItem (experienceItem) {
      this.$emit('complete-item', experienceItem)
    },
    // ERRO!
    incompleteItem (experienceItem) {
      this.$emit('incomplete-item', experienceItem)
    }
  }
}
</script>

<style scoped >
  .b-icon {
    font-size:1.5rem
  }
</style>
