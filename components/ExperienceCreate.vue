<template>
  <section class="experience-create my-3 w-100">
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
    <!-- Create ON -->
    <b-card
      v-show="isCreating"
      bg-variant="white"
      class="mx-lg-5 shadow"
    >
      <!-- Label -->
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
          label-for="experienceTitleCreate"
        >
          <b-form-input
            id="experienceTitleCreate"
            v-model="experienceTitle"
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
          label-for="experienceSubTitleCreate"
        >
          <b-form-input
            id="experienceSubTitleCreate"
            v-model="experienceSubTitle"
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
          label-for="experienceDurationCreate"
        >
          <b-form-input
            id="experienceDurationCreate"
            v-model="experienceDuration"
            type="text"
            :placeholder="content.experienceDurationPlaceholder[language]"
          />
        </b-form-group>
        <!-- Item -->
        <b-form-group
          label-cols-sm="3"
          :label="content.experienceDescription[language]"
          label-align-sm="right"
          label-for="experienceDescriptionCreate"
          :valid-feedback="content.globalThanksC[language]"
          :invalid-feedback="experienceDescriptionInvalid"
          :state="experienceDescriptionState"
        >
          <b-form-textarea
            id="experienceDescriptionCreate"
            v-model="experienceDescription"
            type="textarea"
            rows="3"
            :placeholder="content.experienceDescriptionPlaceholder[language]"
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
  name: 'ExperienceCreate',
  // Parameters received by parent
  props: ['content', 'language'],
  data () {
    // Default items
    return {
      experienceId: '',
      experienceTitle: '',
      experienceSubTitle: '',
      experienceDuration: '',
      experienceDescription: '',
      isCreating: false
    }
  },
  computed: {
    // Validation
    experienceTitleState () {
      return this.experienceTitle.length > 5
    },
    experienceSubTitleState () {
      return this.experienceTitle.length > 5
    },
    experienceDurationState () {
      return this.experienceDuration.length > 4
    },
    experienceDescriptionState () {
      return this.experienceDescription.length > 3
    },
    experienceTitleInvalid () {
      if (this.experienceTitle.length > 0) {
        return this.content.experienceTitleInvalidVoid[this.language]
      }
      return this.content.experienceTitleInvalid[this.language]
    },
    experienceSubTitleInvalid () {
      if (this.experienceTitle.length > 0) {
        return this.content.experienceTitleInvalidVoid[this.language]
      }
      return this.content.experienceTitleInvalid[this.language]
    },
    experienceDurationInvalid () {
      if (this.experienceDuration.length > 0) {
        return this.content.experienceDurationInvalidVoid[this.language]
      }
      return this.content.experienceDurationInvalid[this.language]
    },
    experienceDescriptionInvalid () {
      if (this.experienceDescription.length > 0) {
        return this.content.experienceDescriptionInvalidVoid[this.language]
      }
      return this.content.experienceDescriptionInvalid[this.language]
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
      if (this.experienceTitle.length > 5 && this.experienceDuration.length > 4 && this.experienceDescription.length > 3) {
        const experienceId = this.experienceId
        const experienceTitle = this.experienceTitle
        const experienceSubTitle = this.experienceSubTitle
        const experienceDuration = this.experienceDuration
        const experienceDescription = this.experienceDescription
        // Pass to a parent method
        this.$emit('create-experience-item', {
          experienceId,
          experienceTitle,
          experienceSubTitle,
          experienceDuration,
          experienceDescription,
          experienceCompleted: false
        })
        // Reset after emit
        this.experienceId = ''
        this.experienceTitle = ''
        this.experienceSubTitle = ''
        this.experienceDuration = ''
        this.experienceDescription = ''
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
