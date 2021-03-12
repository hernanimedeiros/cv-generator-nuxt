<template>
  <section class="profile my-5 w-100">
    <!-- Label -->
    <b-card
      :title="content.profileCardTitle[language]"
      :sub-title="content.profileCardSubTitle[language]"
      bg-variant="light"
      class="mx-lg-5 shadow"
    >
      <!-- List items -->
      <ProfileList
        :profile-items="profileItems"
        :language="language"
        :content="content"
      />
    </b-card>
  </section>
</template>

<script>
// Import
import ProfileList from '@/components/ProfileList.vue'
// Export
export default {
  // Name and components
  name: 'Profile',
  components: {
    ProfileList
  },
  // Parameters received by parent
  props: ['content', 'language'],
  data () {
    return {
      // Default items
      profileItems: [
        {
          profilePhoto: '',
          profileFirstName: this.content.profileFirstNameDefault[this.language],
          profileLastName: this.content.profileLastNameDefault[this.language],
          profilePosition: this.content.profilePositionDefault[this.language],
          profilePhone: this.content.profilePhoneDefault[this.language],
          profileEmail: this.content.profileEmailDefault[this.language],
          profileAddress: this.content.profileAddressDefault[this.language],
          profileAbout: this.content.profileAboutDefault[this.language],
          profileStrength: this.content.profileStrengthDefault[this.language],
          profileSocialNetwork: this.content.profileSocialNetworkDefault[this.language],
          profileHobbie: this.content.profileHobbieDefault[this.language],
          profileCompleted: false
        }
      ]
    }
  }
}
</script>

<style>
</style>
