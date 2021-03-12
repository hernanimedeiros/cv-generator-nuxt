<template>
  <section class="cv-form mt-5 w-100">
    <Profile id="profileId" :language="language" :content="content" />
    <Experience id="experienceId" :language="language" :content="content" />
    <Skill id="skillId" :language="language" :content="content" />
    <Education id="educationId" :language="language" :content="content" />
    <Course id="courseId" :language="language" :content="content" />
  </section>
</template>

<script>
// Import
import Profile from '@/components/Profile.vue'
import Skill from '@/components/Skill.vue'
import Experience from '@/components/Experience.vue'
import Education from '@/components/Education.vue'
import Course from '@/components/Course.vue'
// Export
export default {
  // Name and components
  name: 'CvForm',
  components: {
    Profile,
    Skill,
    Experience,
    Education,
    Course
  },
  // Parameters received by parent
  props: ['content', 'language']
}
</script>

<style>
</style>
