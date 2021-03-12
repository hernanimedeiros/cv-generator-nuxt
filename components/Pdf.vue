<template>
  <b-container class="static-item wrapper">
    <b-row>
      <!-- Sidebar -->
      <b-col
        v-for="(elementProfile, index) in getProfile"
        :key="index"
        :style="{ background: getOptions[0].sidebarWrapperBackground, color: getOptions[0].sidebarWrapperColor }"
        class="sidebar-wrapper"
      >
        <!-- Personal VIP information -->
        <div class="profile-container px-0">
          <!-- Profile photo -->
          <b-avatar
            :src="getProfile[0].profilePhoto"
            class="my-3"
            size="120px"
          />
          <!-- Name and Posittion -->
          <h1 class="name">
            {{ elementProfile.profileFirstName }}
            <br>
            {{ elementProfile.profileLastName }}
          </h1>
          <h2 class="tagline">
            {{ elementProfile.profilePosition }}
          </h2>
        </div>
        <!-- Contacts -->
        <div class="container-block">
          <ul class="list-unstyled contact-list">
            <!-- Email -->
            <li>
              <b-icon icon="mailbox" />
              <a
                :href="mailLink"
                target="_blank"
              >
                {{ elementProfile.profileEmail }}
              </a>
            </li>
            <!-- Phone -->
            <li>
              <b-icon icon="telephone" />
              <a
                :href="phoneLink"
                target="_blank"
              >
                {{ elementProfile.profilePhone }}
              </a>
            </li>
            <!-- Adress -->
            <li>
              <b-icon icon="house" />
              {{ elementProfile.profileAddress }}
            </li>
          </ul>
        </div>
        <!-- Strengths -->
        <div class="container-block">
          <b-icon
            class="mb-2"
            icon="award"
            scale="1.5"
          />
          <h2 class="container-block-title">
            {{ content.profileStrength[language] }}
          </h2>
          <ul
            v-for="(elementStrength, index) in elementProfile.profileStrength"
            :key="index"
            class="list-unstyled contact-list"
          >
            <li>
              {{ elementStrength }}
            </li>
          </ul>
        </div>
        <!-- Social network links -->
        <div class="container-block">
          <b-icon
            class="mb-2"
            icon="broadcast"
            scale="1.5"
            animation="throb"
          />
          <h2 class="container-block-title">
            {{ content.profileSocialNetwork[language] }}
          </h2>
          <ul
            v-for="(elementSocialNetwork, index) in elementProfile.profileSocialNetwork"
            :key="index"
            class="list-unstyled contact-list"
          >
            <li class="small">
              {{ elementSocialNetwork }}
            </li>
          </ul>
        </div>
        <!-- Hobbies -->
        <div class="container-block">
          <b-icon
            class="mb-2"
            icon="bicycle"
            scale="1.5"
            animation="cylon"
          />
          <h2 class="container-block-title">
            {{ content.profileHobbie[language] }}
          </h2>
          <ul
            v-for="(elementHobbie, index) in elementProfile.profileHobbie"
            :key="index"
            class="list-unstyled contact-list"
          >
            <li>
              {{ elementHobbie }}
            </li>
          </ul>
        </div>
      </b-col>
      <!-- Main section -->
      <b-col
        class="main-wrapper pl-5"
      >
        <!-- About me -->
        <section class="section mt-5">
          <b-icon
            icon="person-fill"
            scale="1.5"
          />
          <h2 class="section-title">
            {{ content.profileAbout[language] }}
          </h2>
          <!-- In this moment array is not needed but this implementation can be usefull in future versions-->
          <div
            v-for="(elementProfile, index) in getProfile"
            :key="index"
          >
            <p> {{ elementProfile.profileAbout }} </p>
          </div>
        </section>
        <!-- Experience -->
        <section class="mt-5">
          <!-- Label -->
          <div class="d-flex">
            <b-icon
              class="ml-3"
              icon="briefcase-fill"
              scale="1.5"
            />
            <h2 class="section-title ml-3">
              {{ content.experienceTitle[language] }}
            </h2>
          </div>
          <!-- Items -->
          <div
            v-for="(elementExperience, index) in getExperience"
            :key="index"
          >
            <div>
              <h3 class="info-title">
                {{ elementExperience.experienceSubTitle }}
              </h3>
              <div class="d-flex justify-content-left info-secondary">
                <span class="pr-3">
                  {{ elementExperience.experienceTitle }}
                </span>
                {{ " | " }}
                <span class="pl-3">
                  {{ elementExperience.experienceDuration }}
                </span>
              </div>
            </div>
            <div>
              <p>{{ elementExperience.experienceDescription }}</p>
            </div>
          </div>
        </section>
        <!-- Skill -->
        <section class="mt-5">
          <!-- Label -->
          <div class="d-flex">
            <b-icon
              class="ml-3"
              icon="person-lines-fill"
              scale="1.5"
            />
            <h2 class="section-title ml-3">
              {{ content.skillTitle[language] }}
            </h2>
          </div>
          <!-- Items -->
          <div
            v-for="(elementSkill, index) in getSkill"
            :key="index"
          >
            <div>
              <div>
                <h3 class="info-title">
                  {{ elementSkill.skillTitle }}
                  <span v-show="getOptions[0].rating">
                    <b-form-rating
                      :value="elementSkill.skillRating"
                      readonly
                      precision="0"
                      variant="warning"
                      inline
                      class="border-0 rating-bg"
                    />
                  </span>
                </h3>
              </div>
            </div>
            <div>
              <p>
                {{ elementSkill.skillDescription }}
              </p>
            </div>
          </div>
        </section>
        <!-- Course -->
        <section class="mt-5">
          <!-- Label -->
          <div class="d-flex">
            <b-icon
              class="ml-3"
              icon="pencil-fill"
              scale="1.5"
            />
            <h2 class="section-title ml-3">
              {{ content.courseTitle[language] }}
            </h2>
          </div>
          <!-- Items -->
          <div
            v-for="(elementCourse, index) in getCourse"
            :key="index"
          >
            <div>
              <div class="d-flex justify-content-left">
                <h3 class="info-title pr-3">
                  {{ elementCourse.courseTitle }}
                </h3>
                <div class="info-secondary pl-3">
                  ( {{ elementCourse.courseDuration }} )
                </div>
              </div>
            </div>
            <div>
              <p>
                {{ elementCourse.courseDescription }}
              </p>
            </div>
          </div>
        </section>

        <!-- Education -->
        <section class="mt-5">
          <!-- Label -->
          <div class="d-flex">
            <b-icon
              class="ml-3"
              icon="book-half"
              scale="1.5"
            />
            <h2 class="section-title ml-3">
              {{ content.educationTitle[language] }}
            </h2>
          </div>
          <div>
            <div
              v-for="(elementEducation, index) in getEducation"
              :key="index"
            >
              <h3 class="info-title">
                {{ elementEducation.educationDescription }}
              </h3>
              <div class="d-flex justify-content-left info-secondary">
                <span class="info-secondary pr-3">
                  {{ elementEducation.educationTitle }}
                </span>|
                <span class="pl-3">
                  {{ elementEducation.educationDuration }}
                </span>
              </div>
            </div>
          </div>
        </section>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
// Import
import { mapGetters } from 'vuex'
// Export
export default {
  // Name and components
  name: 'Static',
  // Properties received from parent
  props: ['content', 'language'],
  computed: {
    // Shortcut to mutations
    ...mapGetters({
      getPreferences: 'preferences/get',
      getProfile: 'profile/get',
      getSkill: 'skill/get',
      getExperience: 'experience/get',
      getEducation: 'education/get',
      getCourse: 'course/get',
      getOptions: 'options/get'
    }),
    // Not used
    preferencesCheck () {
      return this.getPreferences
    },
    // Acess to store (with map)
    profileItemsCheck () {
      return this.getProfile
    },
    skillItemsCheck () {
      return this.getSkill
    },
    experienceItemsCheck () {
      return this.getExperience
    },
    educationItemsCheck () {
      return this.getEducation
    },
    courseItemsCheck () {
      return this.getCourse
    },
    optionsCheck () {
      return this.getOptions
    },
    // Link modifiers
    mailLink () {
      const email = String(this.profileItemsCheck.profileEmail).replace(/\s+/g, '')
      const emailPrefix = 'mailto:'
      const emailSubject = '?subject=C.V.%msg:'
      return emailPrefix + email + emailSubject
    },
    phoneLink () {
      const phone = String(this.profileItemsCheck.profileEmail).replace(/\s+/g, '')
      const phonePrefix = 'tel:'
      return phonePrefix + phone
    }
  }
}
</script>

<style scoped >
  b-container {
    font-family: Roboto, sans-serif;
    font-size: 16px;
    margin: 0;
    padding: 0;
  }

  a {
    text-decoration: none;
    color: inherit;
  }

  a:hover {
    text-decoration: none;
  }

  a:focus {
    text-decoration: none;
  }

  p {
    line-height: 1.5;
    font-size: 1rem;
  }

  .wrapper {
    max-width:100%;
    margin-right:2rem;
    }

  .sidebar-wrapper {
    background: lightseagreen;
    text-align: center;
    color: #ffffff;
    max-width: 33%;
  }

  .sidebar-wrapper a {
    text-decoration: none;
  }

  .sidebar-wrapper .name {
    font-size: 2rem;
    font-weight: 900;
    margin-top: 0;
    margin-bottom: 0.75rem;
  }

  .sidebar-wrapper .tagline {
    font-size: 1rem;
    font-weight: 300;
    margin-bottom: 1rem;
  }

  .sidebar-wrapper .contact-list li {
    margin-bottom: 1rem;
  }

  .sidebar-wrapper .contact-list li:last-child {
    margin-bottom: 0;
  }

  .sidebar-wrapper .container-block {
    padding: 1rem;
  }

  .sidebar-wrapper .container-block-title {
    text-transform: uppercase;
    font-size: 1rem;
    font-weight: 700;
    margin-top: 0;
    margin-bottom: 1rem;
  }

  .main-wrapper {
    text-align: center;
    min-height:100vh;
    max-width:66%;
  }

  .main-wrapper p{
    text-align: justify;
  }

  .main-wrapper .section-title {
    text-transform: uppercase;
    font-size: 20px;
    font-weight: 500;
    position: relative;
    margin-top: 0;
    margin-bottom: 20px;
  }

  .info-title {
    font-size: 1.25rem;
    font-weight: 700;
    text-align: left;
  }

  .info-secondary {
    font-size: 1rem;
    font-style: italic;
    text-align: left;
    color: dimgrey
  }

  .rating-bg {
    background-color: inherit;
  }
</style>
