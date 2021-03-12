<template>
  <section class="profile-list w-100">
    <!-- Completed stats. Array interactions not necessary now but can be usefull in future versions -->
    <ProfileListItem
      v-for="(profileItem,index) in profileItems"
      :key="index"
      :profile-item="profileItem"
      :language="language"
      :content="content"
      @complete-item="completeItem"
      @incomplete-item="incompleteItem"
    />
  </section>
</template>

<script>
// Import
import ProfileListItem from '@/components/ProfileListItem.vue'
import { mapMutations } from 'vuex'
// Export
export default {
  // Name and components
  name: 'ProfileList',
  components: {
    ProfileListItem
  },
  // Properties received from parent
  props: ['profileItems', 'content', 'language'],
  methods: {
    // Shortcut to mutations
    ...mapMutations({
      change: 'profile/set'
    }),
    // Methods for actions
    completeItem (profileItem) {
      // Select element to be mark as completed
      const itemIndex = this.profileItems.indexOf(profileItem)
      // Modify state of item
      this.profileItems[itemIndex].profileCompleted = true
      // this.$store.commit('profile/set', this.profileItems)
      this.change(this.profileItems)
    },
    incompleteItem (profileItem) {
      // Select element to be mark as completed
      const itemIndex = this.profileItems.indexOf(profileItem)
      // Modify state of item
      this.profileItems[itemIndex].profileCompleted = false
      // this.$store.commit('profile/set', this.profileItems.filter((profileItem) => { return profileItem.profileCompleted === true }))
      this.change(this.profileItems.filter((profileItem) => { return profileItem.profileCompleted === true }))
    }
  }
}
</script>

<style>
</style>
