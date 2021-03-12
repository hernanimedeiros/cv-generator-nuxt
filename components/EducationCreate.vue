<template>
  <section class="education-create my-3 w-100">
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
          label-for="educationTitleCreate"
        >
          <b-form-input
            id="educationTitleCreate"
            v-model="educationTitle"
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
          label-for="educationDurationCreate"
        >
          <b-form-input
            id="educationDurationCreate"
            v-model="educationDuration"
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
          label-for="educationDescriptionCreate"
        >
          <b-form-textarea
            id="educationDescriptionCreate"
            v-model="educationDescription"
            type="textarea"
            rows="3"
            :placeholder="content.educationDescriptionPlaceholder[language]"
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
  name: 'EducationCreate',
  // Parameters received by parent
  props: ['content', 'language'],
  data () {
    // Default items
    return {
      educationId: '',
      educationTitle: '',
      educationDuration: '',
      educationDescription: '',
      isCreating: false
    }
  },
  computed: {
    // Validation
    educationTitleState () {
      return this.educationTitle.length > 5
    },
    educationDurationState () {
      return this.educationDuration.length > 4
    },
    educationDescriptionState () {
      return this.educationDescription.length > 3
    },
    educationTitleInvalid () {
      if (this.educationTitle.length > 0) {
        return this.content.educationTitleInvalidVoid[this.language]
      }
      return this.content.educationTitleInvalid[this.language]
    },
    educationDurationInvalid () {
      if (this.educationDuration.length > 0) {
        return this.content.educationDurationInvalidVoid[this.language]
      }
      return this.content.educationDurationInvalid[this.language]
    },
    educationDescriptionInvalid () {
      if (this.educationDescription.length > 0) {
        return this.content.educationDescriptionInvalidVoid[this.language]
      }
      return this.content.educationDescriptionInvalid[this.language]
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
      if (this.educationTitle.length > 5 && this.educationDuration.length > 4 && this.educationDescription.length > 3) {
        const educationId = this.educationId
        const educationTitle = this.educationTitle
        const educationDuration = this.educationDuration
        const educationDescription = this.educationDescription
        // Pass to a parent method
        this.$emit('create-education-item', {
          educationId,
          educationTitle,
          educationDuration,
          educationDescription,
          educationCompleted: false
        })
        // Reset after emit
        this.educationId = ''
        this.educationTitle = ''
        this.educationDuration = ''
        this.educationDescription = ''
        this.isCreating = false
      }
    }
  }
}
</script>

<style scoped >
  .b-icon{
    font-size:1.5rem
  }
</style>
