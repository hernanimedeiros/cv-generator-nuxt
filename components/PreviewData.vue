<template>
  <section class="preview-data my-5 w-100">
    <!-- Bottom alert -->
    <b-alert
      v-model="showBottomAlert"
      class="position-fixed fixed-bottom m-0 rounded-0"
      style="z-index: 2000;"
      variant="warning"
      dismissible
    >
      {{ content.previewDataAlert[language] }}
    </b-alert>
    <b-card
      :title="content.previewDataLabel[language]"
      :sub-title="content.previewDataSubLabel[language]"
      bg-variant="light"
      class="mx-lg-5 shadow"
    >
      <!-- Show preview toggle -->
      <b-button
        variant="outline-secondary"
      >
        <div class="d-flex justify-content-center">
          <!-- Label -->
          <span class="mr-3">
            {{ "Show data" }}
          </span>
          <!-- Show action -->
          <div
            v-show="!isPreview"
            @click="showPreview"
          >
            <b-icon
              icon="circle-fill"
              variant="outline-danger"
            />
          </div>
          <!-- Hide action-->
          <div
            v-show="isPreview"
            @click="hidePreview"
          >
            <b-icon
              icon="circle-fill"
              variant="success"
            />
          </div>
        </div>
      </b-button>
      <!-- Label -->
      <!-- Hide mode -->
      <b-card
        v-show="!isPreview"
        :title="content.previewDataTitle[language]"
        :sub-title="content.previewDataSubTitle[language]"
        bg-variant="dark"
        class="mx-lg-5 mt-5 shadow text-white"
      >
        <b-col cols="6" class="mx-auto">
          <b-card bg-variant="light" class="mx-auto text-white">
            <pre>{{ "JSON DATA" }}</pre>
          </b-card>
        </b-col>
      </b-card>
      <!-- Show mode -->
      <b-card
        v-show="isPreview"
        title="Data marked as completed:"
        sub-title="JSON format"
        bg-variant="dark"
        class="mx-lg-5 mt-5 shadow text-white"
      >
        <b-col cols="6" class="mx-auto">
          <!-- Item -->
          <p class="mt-3">
            Preferences
          </p>
          <b-card bg-variant="light" class="mx-auto text-white">
            <pre> {{ getPreferences }} </pre>
          </b-card>
          <!-- Item -->
          <p class="mt-3">
            Profile
          </p>
          <b-card bg-variant="light" class="mx-auto text-white">
            <pre> {{ getProfile }} </pre>
          </b-card>
          <!-- Item -->
          <p class="mt-3">
            Skills
          </p>
          <b-card bg-variant="light" class="mx-auto text-white">
            <pre> {{ getSkill }} </pre>
          </b-card>
          <!-- Item -->
          <p class="mt-3">
            Experience
          </p>
          <b-card bg-variant="light" class="mx-auto text-white">
            <pre> {{ getExperience }} </pre>
          </b-card>
          <!-- Item -->
          <p class="mt-3">
            Education
          </p>
          <b-card bg-variant="light" class="mx-auto text-white">
            <pre> {{ getEducation }} </pre>
          </b-card>
          <!-- Item -->
          <p class="mt-3">
            Courses
          </p>
          <b-card bg-variant="light" class="mx-auto text-white">
            <pre> {{ getCourse }} </pre>
          </b-card>
          <!-- Item -->
          <p class="mt-3">
            Options
          </p>
          <b-card bg-variant="light" class="mx-auto text-white">
            <pre> {{ getOptions }} </pre>
          </b-card>
        </b-col>
      </b-card>
    </b-card>
  </section>
</template>

<script>
// Import
import { mapGetters } from 'vuex'
// Export
export default {
  // Name and components
  name: 'PreviewData',
  // Properties received from parent
  props: ['content', 'language'],
  data () {
    return {
      // Default items
      isPreview: false,
      showBottomAlert: false
    }
  },
  computed: {
    // Shortcut to mutations
    ...mapGetters({
      getPreferences: 'preferences/get',
      getOptions: 'options/get',
      getProfile: 'profile/get',
      getCourse: 'course/get',
      getEducation: 'education/get',
      getExperience: 'experience/get',
      getSkill: 'skill/get'
    })
  },
  methods: {
    // Methods for actions
    showPreview () {
      this.isPreview = true
      this.showBottomAlert = true
    },
    hidePreview () {
      this.isPreview = false
    }
  }
}
</script>

<style>
</style>
