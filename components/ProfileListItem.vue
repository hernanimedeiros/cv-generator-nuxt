<template>
  <section class="profile-list-item my-3 w-100">
    <!-- Show mode -->
    <b-card
      v-show="!isEditing"
      bg-variant="white"
      class="mx-lg-5 shadow"
    >
      <b-card-body>
        <!-- Photo load mode -->
        <b-avatar
          v-show="!profilePhoto"
          :src="require('../assets/profile_photo.png')"
          class="my-3 shadow"
          size="170px"
        />
        <!-- Photo loaded mode -->
        <b-avatar
          v-show="profilePhoto"
          :src="profilePhotoUrl"
          class="my-3"
          size="170px"
        />
        <!-- Profile presentation - Main items -->
        <!-- First name and last name -->
        <b-card-title> {{ profileItem.profileFirstName }} {{ profileItem.profileLastName }} ({{ profileItem.profilePosition }})</b-card-title>
        <b-card-sub-title class="mb-2">
          <!-- Phone and mail -->
          {{ profileItem.profilePhone }} | {{ profileItem.profileEmail }}
        </b-card-sub-title>
        <!-- Address -->
        <b-card-text> {{ profileItem.profileAddress }} </b-card-text>
        <!-- About -->
        <b-card-text> {{ profileItem.profileAbout }} </b-card-text>
      </b-card-body>
    </b-card>
    <!-- Profile presentation - Secondary items -->
    <b-card-group
      v-show="!isEditing"
      class="mx-lg-5"
    >
      <!-- Strengths label -->
      <b-card
        :header="content.profileStrength[language]"
        bg-variant="white"
        class="mx-lg-1 my-3 shadow"
      >
        <!-- Strengths items -->
        <b-list-group
          v-for="(elementStrength,index) in profileItem.profileStrength"
          :key="index"
        >
          <b-list-group-item> {{ elementStrength }} </b-list-group-item>
        </b-list-group>
      </b-card>
      <!-- Social network label -->
      <b-card
        :header="content.profileSocialNetwork[language]"
        bg-variant="white"
        class="mx-lg-1 my-3  shadow"
      >
        <!-- Social network items -->
        <b-list-group
          v-for="(elementSocialNetwork,index) in profileItem.profileSocialNetwork"
          :key="index"
        >
          <b-list-group-item> {{ elementSocialNetwork }} </b-list-group-item>
        </b-list-group>
      </b-card>
      <!-- Hobbies label -->
      <b-card
        :header="content.profileHobbie[language]"
        bg-variant="white"
        class="mx-lg-1 my-3 shadow"
      >
        <!-- Hobbies items -->
        <b-list-group
          v-for="(elementHobbie,index) in profileItem.profileHobbie"
          :key="index"
        >
          <b-list-group-item> {{ elementHobbie }} </b-list-group-item>
        </b-list-group>
      </b-card>
    </b-card-group>
    <!-- Edit and delete buttons -->
    <div v-show="!isEditing" class="my-3">
      <span>
        <b-icon
          icon="pencil-square"
          class="b-icon-up-simple"
          @click="showForm"
        />
      </span>
    </div>
    <!-- Complete and incomplete state toggle -->
    <div class="d-flex justify-content-end">
      <b-button
        v-show="!isEditing"
        id="tooltip-target-1"
        variant="outline-secondary"
      >
        <div class="d-flex justify-content-end">
          <!-- Label -->
          <span class="mr-3">
            {{ content.completedLabel[language] }}
          </span>
          <!-- Incomplete -->
          <div
            v-show="!isEditing && profileItem.profileCompleted"
            @click="incompleteItem(profileItem) ; incompletedToast()"
          >
            <b-icon
              icon="circle-fill"
              variant="success"
            />
          </div>
          <!-- Complete -->
          <div
            v-show="!isEditing && !profileItem.profileCompleted"
            @click="completeItem(profileItem) ; completedToast()"
          >
            <b-icon
              icon="circle-fill"
              variant="outline-danger"
            />
          </div>
        </div>
      </b-button>
      <!-- Tooltip -->
      <b-tooltip target="tooltip-target-1" placement="left" triggers="hover">
        {{ content.completedInfo[language] }}
      </b-tooltip>
    </div>
    <!-- Edition mode -->
    <b-card v-show="isEditing" bg-variant="light" class="mx-lg-5 shadow">
      <!-- Form -->
      <b-form-group
        label-cols-lg="3"
        :label="content.profileLabel[language]"
        label-size="lg"
        label-class="font-weight-bold pt-0"
        class="mb-0"
      >
        <!-- Photo preview-->
        <b-form-group
          label-cols-sm="3"
          label-align-sm="right"
          label-for="photoPreview"
        >
          <b-input-group>
            <b-avatar
              v-show="!profilePhoto"
              id="profilePreview"
              :src="require('../assets/profile_photo.png')"
              class="my-3"
              size="170px"
            />
            <!-- Photo loaded mode -->
            <b-avatar
              v-show="profilePhoto"
              id="profilePreview"
              :src="profilePhotoUrl"
              class="my-3"
              size="170px"
            />
          </b-input-group>
        </b-form-group>
        <!-- Photo load -->
        <b-form-group
          label-cols-sm="3"
          :label="content.profilePhotoLabel[language]"
          label-align-sm="right"
          label-for="profilePhoto"
        >
          <!-- Photo -->
          <b-input-group>
            <b-form-file
              id="profilePhoto"
              v-model="profilePhoto"
              :placeholder="content.profilePhotoPlaceholder[language]"
              :drop-placeholder="content.profilePhotoDropPlaceholder[language]"
              :state="Boolean(profilePhoto)"
              accept=".jpg, .jpeg, .png"
              @change="onFileChange"
            />
            <!-- Reset photo loaded -->
            <b-input-group-append>
              <b-button @click="profilePhoto = null">
                {{ content.cancel[language] }}
              </b-button>
            </b-input-group-append>
          </b-input-group>
        </b-form-group>
        <!-- First name -->
        <b-form-group
          label-cols-sm="3"
          :label="content.profileFirstName[language]"
          label-align-sm="right"
          label-for="profileFirstName"
          :valid-feedback="content.globalThanksA[language]"
          :invalid-feedback="profileFirstNameInvalid"
          :state="profileFirstNameState"
        >
          <b-form-input
            id="profileFirstName"
            v-model="profileItem.profileFirstName"
            type="text"
            :placeholder="content.profileFirstNamePlaceholder[language]"
          />
        </b-form-group>
        <!-- Last name -->
        <b-form-group
          label-cols-sm="3"
          label-align-sm="right"
          label-for="profileLastName"
          :label="content.profileLastName[language]"
          :valid-feedback="content.globalThanksA[language]"
          :invalid-feedback="profileLastNameInvalid"
          :state="profileLastNameState"
        >
          <b-form-input
            id="profileLastName"
            v-model="profileItem.profileLastName"
            type="text"
            :placeholder="content.profileLastNamePlaceholder[language]"
          />
        </b-form-group>
        <!-- Position -->
        <b-form-group
          label-cols-sm="3"
          :label="content.profilePosition[language]"
          label-align-sm="right"
          label-for="profilePosition"
          :valid-feedback="content.globalThanksA[language]"
          :invalid-feedback="profilePositionInvalid"
          :state="profilePositionState"
        >
          <b-form-input
            id="profilePosition"
            v-model="profileItem.profilePosition"
            type="text"
            :placeholder="content.profilePositionPlaceholder[language]"
          />
        </b-form-group>
        <!-- Phone -->
        <b-form-group
          label-cols-sm="3"
          :label="content.profilePhone[language]"
          label-align-sm="right"
          label-for="profilePhone"
          :valid-feedback="content.globalThanksA[language]"
          :invalid-feedback="profilePhoneInvalid"
          :state="profilePhoneState"
        >
          <b-form-input
            id="profilePhone"
            v-model="profileItem.profilePhone"
            type="tel"
            :placeholder="content.profilePhonePlaceholder[language]"
          />
        </b-form-group>
        <!-- E-mail -->
        <b-form-group
          label-cols-sm="3"
          :label="content.profileEmail[language]"
          label-align-sm="right"
          label-for="profileEmail"
          :valid-feedback="content.globalThanksA[language]"
          :invalid-feedback="profileEmailInvalid"
          :state="profileEmailState"
        >
          <b-form-input
            id="profileEmail"
            v-model="profileItem.profileEmail"
            type="email"
            :placeholder="content.profileEmailPlaceholder[language]"
          />
        </b-form-group>
        <!-- Address -->
        <b-form-group
          label-cols-sm="3"
          :label="content.profileAddress[language]"
          label-align-sm="right"
          label-for="profileAddress"
          :valid-feedback="content.globalThanksA[language]"
          :invalid-feedback="profileAddressInvalid"
          :state="profileAddressState"
        >
          <b-form-input
            id="profileAddress"
            v-model="profileItem.profileAddress"
            type="text"
            :placeholder="content.profileAddressPlaceholder[language]"
          />
        </b-form-group>
        <!-- About -->
        <b-form-group
          label-cols-sm="3"
          :label="content.profileAbout[language]"
          label-align-sm="right"
          label-for="profileAbout"
        >
          <b-form-textarea
            id="profileAbout"
            v-model="profileItem.profileAbout"
            type="text"
            rows="5"
            :placeholder="content.profileAboutPlaceholder[language]"
          />
        </b-form-group>
        <!-- Strength -->
        <b-form-group
          label-cols-sm="3"
          :label="content.profileStrength[language]"
          label-align-sm="right"
          label-for="profileStrength"
        >
          <b-form-tags
            id="profileStrength"
            v-model="profileItem.profileStrength"
            type="text"
            :value="content.profileStrengthPlaceholder[language]"
          />
        </b-form-group>
        <!-- Socila Network -->
        <b-form-group
          label-cols-sm="3"
          :label="content.profileSocialNetwork[language]"
          label-align-sm="right"
          label-for="profileSocialNetwork"
        >
          <b-form-tags
            id="profileSocialNetwork"
            v-model="profileItem.profileSocialNetwork"
            type="text"
            :value="content.profileSocialNetworkPlaceholder[language]"
          />
        </b-form-group>
        <!-- Hobbie -->
        <b-form-group
          label-cols-sm="3"
          :label="content.profileHobbie[language]"
          label-align-sm="right"
          label-for="profileHobbie"
        >
          <b-form-tags
            id="profileHobbie"
            v-model="profileItem.profileHobbie"
            type="text"
            :value="content.profileHobbiePlaceholder[language]"
          />
        </b-form-group>
      </b-form-group>
      <!-- Confirm changes -->
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
export default {
  name: 'ProfileListItem',
  // Properties received from parent
  props: ['profileItem', 'content', 'language'],
  data () {
    return {
      isEditing: false,
      profilePhoto: null,
      profilePhotoUrl: null
    }
  },
  computed: {
    // Validation
    profileFirstNameState () {
      return this.profileItem.profileFirstName.length > 2
    },
    profileLastNameState () {
      return this.profileItem.profileLastName.length > 2
    },
    profilePositionState () {
      return this.profileItem.profilePosition.length > 2
    },
    profilePhoneState () {
      return this.profileItem.profilePhone.length > 8
    },
    profileEmailState () {
      return this.profileItem.profileEmail.length > 6
    },
    profileAddressState () {
      return this.profileItem.profileAddress.length > 5
    },
    profileFirstNameInvalid () {
      if (this.profileItem.profileFirstName.length > 0) {
        return this.content.profileFirstNameInvalidVoid[this.language]
      }
      return this.content.profileFirstNameInvalid[this.language]
    },
    profileLastNameInvalid () {
      if (this.profileItem.profileLastName.length > 0) {
        return this.content.profileLastNameInvalidVoid[this.language]
      }
      return this.content.profileLastNameInvalid[this.language]
    },
    profilePositionInvalid () {
      if (this.profileItem.profilePosition.length > 0) {
        return this.content.profilePositionInvalidVoid[this.language]
      }
      return this.content.profilePositionInvalid[this.language]
    },
    profilePhoneInvalid () {
      if (this.profileItem.profilePhone.length > 0) {
        return this.content.profilePhoneInvalidVoid[this.language]
      }
      return this.content.profilePhoneInvalid[this.language]
    },
    profileEmailInvalid () {
      if (this.profileItem.profileEmail.length > 0) {
        return this.content.profileEmailInvalidVoid[this.language]
      }
      return this.content.profileEmailInvalid[this.language]
    },
    profileAddressInvalid () {
      if (this.profileItem.profileAddress.length > 0) {
        return this.content.profileAddressInvalidVoid[this.language]
      }
      return this.content.profileAddressInvalid[this.language]
    }

  },
  methods: {
    // Methods to actions
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
    completeItem (profileItem) {
      this.$emit('complete-item', profileItem)
    },
    incompleteItem (profileItem) {
      this.$emit('incomplete-item', profileItem)
    },
    // Composing URL for scr attribute
    onFileChange (profilePhoto) {
      const file = profilePhoto.target.files[0]
      this.profilePhotoUrl = URL.createObjectURL(file)
      this.profileItem.profilePhoto = this.profilePhotoUrl
    }
  }
}
</script>

<style scoped >
  .b-icon {
    font-size:1.5rem
  }
</style>
