<template>
  <section class="preview w-100">
    <b-container fluid class="top-margin" />
    <b-container fluid>
      <b-row>
        <b-col lg="6" class="aside-photo mb-3" />
        <b-col lg="6" class="mb-3">
          <b-card class="shadow" no-body bg-variant="dark" text-variant="white" header-tag="header">
            <template #header>
              <a href="#profileId" class="titleLabel"> {{ content.profileLabel[language] }} </a>
            </template>
            <b-list-group flush>
              <b-list-group-item href="#skillId">
                {{ content.skillLabel[language] }}
              </b-list-group-item>
              <b-list-group-item href="#experienceId">
                {{ content.experienceLabel[language] }}
              </b-list-group-item>
              <b-list-group-item href="#educationId">
                {{ content.educationLabel[language] }}
              </b-list-group-item>
              <b-list-group-item href="#courseId">
                {{ content.courseLabel[language] }}
              </b-list-group-item>
              <b-list-group-item href="#finishId" variant="success">
                {{ content.successLabel[language] }}
              </b-list-group-item>
            </b-list-group>
            <b-card-body>
              <p>
                {{ content.successWish[language] }}
              </p>
            </b-card-body>
          </b-card>
        </b-col>
      </b-row>
    </b-container>
  </section>
</template>

<script>
// Export
export default {
  // Name and components
  name: 'Preview',
  // Properties received from parent
  props: ['content', 'language']
}
</script>

<style scoped>

  .titleLabel {
    text-decoration: none;
    color:whitesmoke;
  }

  .aside-photo {
    /* The image used */
    background-image: url("../assets/people-meeting.jpg");
    /* Height */
    height: 50vh;
    /* Props */
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;
  }

  .top-margin {
    /* Height */
    min-height: 15vh;
  }

  /* Extra small devices (phones, 600px and down) */
  @media only screen and (max-width: 600px) {
    .top-margin {display:none;}
    .aside-photo {padding:0; margin:0}
  }
</style>
