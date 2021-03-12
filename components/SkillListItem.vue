<template>
  <section class="skill-list-item my-3 w-100">
    <!-- Show mode -->
    <b-card
      v-show="!isEditing"
      bg-variant="white"
      class="mx-lg-5 shadow"
    >
      <!-- Data presentation -->
      <b-card-body>
        <b-card-title>
          {{ skillItem.skillTitle }}
        </b-card-title>
        <b-form-rating
          :value="skillItem.skillRating"
          readonly
          precision="0"
          variant="warning"
          inline
          class="border-0"
        />
        <b-card-text>
          {{ skillItem.skillDescription }}
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
            @click="deleteItem(skillItem)"
          />
        </span>
      </div>
      <!-- Complete and incomplete state toggle -->
      <div class="d-flex justify-content-end">
        <b-button
          id="tooltip-target-5"
          variant="outline-secondary"
        >
          <div class="d-flex justify-content-end">
            <!-- Label -->
            <span class="mr-3">
              {{ content.completedLabel[language] }}
            </span>
            <!-- Incomplete -->
            <div
              v-show="!isEditing && skillItem.skillCompleted"
              @click="incompleteItem(skillItem) ; incompletedToast()"
            >
              <b-icon
                icon="circle-fill"
                variant="success"
              />
            </div>
            <!-- Complete -->
            <div
              v-show="!isEditing && !skillItem.skillCompleted"
              @click="completeItem(skillItem) ; completedToast()"
            >
              <b-icon
                icon="circle-fill"
                variant="outline-danger"
              />
            </div>
          </div>
        </b-button>
        <!-- Tooltip -->
        <b-tooltip target="tooltip-target-5" placement="left" triggers="hover">
          {{ content.completedInfo[language] }}
        </b-tooltip>
      </div>
    </b-card>

    <!-- Edition mode -->
    <b-card v-show="isEditing" bg-variant="light" class="mx-lg-5 shadow">
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
          label-for="skillTitle"
        >
          <b-form-input
            id="skillTitle"
            v-model="skillItem.skillTitle"
            :placeholder="content.skillTitlePlaceholder[language]"
            type="text"
          />
        </b-form-group>
        <!-- Item -->
        <b-form-group
          :label="content.skillRating[language]"
          label-cols-sm="3"
          label-align-sm="right"
          label-for="skillRating"
        >
          <b-form-rating
            id="skillRating"
            v-model="skillItem.skillRating"
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
          label-for="skillDescription"
        >
          <b-form-textarea
            id="skillDescription"
            v-model="skillItem.skillDescription"
            :placeholder="content.skillDescriptionPlaceholder[language]"
            type="text"
            rows="2"
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
  name: 'SkillListItem',
  // Properties received from parent
  props: ['skillItem', 'content', 'language'],
  data () {
    return {
      // Default items
      isEditing: false
    }
  },
  computed: {
    // Validation
    skillTitleState () {
      return this.skillItem.skillTitle.length > 5
    },
    skillDescriptionState () {
      return this.skillItem.skillDescription.length > 5
    },
    skillTitleInvalid () {
      if (this.skillItem.skillTitle.length > 0) {
        return this.content.skillTitleInvalidVoid[this.language]
      }
      return this.content.skillTitleInvalid[this.language]
    },
    skillDescriptionInvalid () {
      if (this.skillItem.skillDescription.length > 0) {
        return this.content.skillDescriptionInvalidVoid[this.language]
      }
      return this.content.skillDescriptionInvalid[this.language]
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
    deleteItem (skillItem) {
      this.$emit('delete-item', skillItem)
    },
    completeItem (skillItem) {
      this.$emit('complete-item', skillItem)
    },
    incompleteItem (skillItem) {
      this.$emit('incomplete-item', skillItem)
    }
  }
}
</script>

<style scoped >
  .b-icon {
    font-size:1.5rem
  }
</style>
