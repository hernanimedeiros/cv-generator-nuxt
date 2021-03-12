<template>
  <section class="skill-create my-3 w-100">
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
        :label="content.skillLabel[language]"
        label-cols-lg="3"
        label-size="lg"
        label-class="font-weight-bold pt-0"
        class="mb-0"
      >
        <!-- Item -->
        <b-form-group
          :label="content.skillTitle[language]"
          :valid-feedback="content.globalThanksA[language]"
          :invalid-feedback="skillTitleInvalid"
          :state="skillTitleState"
          label-cols-sm="3"
          label-align-sm="right"
          label-for="skillTitleCreate"
        >
          <b-form-input
            id="skillTitleCreate"
            v-model="skillTitle"
            :placeholder="content.skillTitlePlaceholder[language]"
            type="text"
          />
        </b-form-group>
        <!-- Item -->
        <b-form-group
          :label="content.skillRating[language]"
          label-cols-sm="3"
          label-align-sm="right"
          label-for="skillRatingCreate"
        >
          <b-form-rating
            id="skillRatingCreate"
            v-model="skillRating"
            precision="0"
            show-clear
            show-value
            variant="warning"
          />
        </b-form-group>
        <!-- Item -->
        <b-form-group
          :label="content.skillDescription[language]"
          :valid-feedback="content.globalThanksC[language]"
          :invalid-feedback="skillDescriptionInvalid"
          :state="skillDescriptionState"
          label-cols-sm="3"
          label-align-sm="right"
          label-for="skillDescriptionCreate"
        >
          <b-form-textarea
            id="skillDescriptionCreate"
            v-model="skillDescription"
            type="textarea"
            rows="2"
            :placeholder="content.skillDescriptionPlaceholder[language]"
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
  name: 'SkillCreate',
  // Parameters received by parent
  props: ['content', 'language'],
  data () {
    // Default items
    return {
      skillTitle: '',
      skillRating: 5,
      skillDescription: '',
      isCreating: false
    }
  },
  computed: {
    // Validation
    skillTitleState () {
      return this.skillTitle.length > 5
    },
    skillDescriptionState () {
      return this.skillDescription.length > 5
    },
    skillTitleInvalid () {
      if (this.skillTitle.length > 0) {
        return this.content.skillTitleInvalidVoid[this.language]
      }
      return this.content.skillTitleInvalid[this.language]
    },
    skillDescriptionInvalid () {
      if (this.skillDescription.length > 0) {
        return this.content.skillDescriptionInvalidVoid[this.language]
      }
      return this.content.skillDescriptionInvalid[this.language]
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
      if (this.skillTitle.length > 5 && this.skillDescription.length > 5) {
        const skillId = this.skillId
        const skillTitle = this.skillTitle
        const skillRating = this.skillRating
        const skillDescription = this.skillDescription
        // Pass to a parent method
        this.$emit('create-skill-item', {
          skillId,
          skillTitle,
          skillRating,
          skillDescription,
          skillCompleted: false
        })
        // Reset after emit
        this.skillId = ''
        this.skillTitle = ''
        this.skillRating = 5
        this.skillDescription = ''
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
