<template>
  <section class="home bg-grey-linear w-100">
    <b-container fluid>
      <!-- Margin top -->
      <div class="top-margin" />
      <div class="my-5">
        <!-- Header -->
        <b-jumbotron class="bg-transparent" text-variant="white">
          <template #header>
            <span class="big-title">
              {{ "CV GENERAT" }}<b-icon icon="globe" />{{ "R" }}
            </span>
          </template>
          <template #lead>
            <h1 class="big-sub-title">
              {{ content.metaHomeDescription[language] }}
            </h1>
            <h2>
              {{ content.homeSubTitle[language] }}
            </h2>
          </template>
          <p>
            {{ content.homeDescription[language] }}
          </p>
          <b-button class="button-purple">
            <nuxtLink to="/Cv" class="nav-link text-white">
              {{ content.homeButton[language] }}
            </nuxtLink>
          </b-button>
        </b-jumbotron>
      </div>
    </b-container>
    <!-- Main  -->
    <b-container fluid class="my-5">
      <b-row>
        <b-col lg="6" class="text-white mt-5">
          <h2>
            {{ content.homeBoxATitle[language] }}
          </h2>
          <p>
            {{ content.homeBoxADescription[language] }}
          </p>
        </b-col>
        <b-col lg="6" class="text-white mt-5">
          <h2>
            {{ content.homeBoxBTitle[language] }}
          </h2>
          <p>
            {{ content.homeBoxBDescription[language] }}
          </p>
        </b-col>
      </b-row>
      <b-row>
        <b-col lg="6" class="text-white mt-5">
          <h2>
            {{ content.homeBoxCTitle[language] }}
          </h2>
          <p>
            {{ content.homeBoxCDescription[language] }}
          </p>
        </b-col>
        <b-col lg="6" class="text-white mt-5">
          <h2>
            {{ content.homeBoxDTitle[language] }}
          </h2>
          <p>
            {{ content.homeBoxDDescription[language] }}
          </p>
        </b-col>
      </b-row>
    </b-container>
    <div class="parallax-home w-100" />
    <!-- Cards -->
    <b-container fluid class="my-5">
      <b-card-group deck>
        <b-card bg-variant="transparent" text-variant="white" :header="content.profileLabel[language]" class="text-center my-3">
          <b-icon icon="person-fill" variant="light" class="mx-auto my-auto icon-inside" />
        </b-card>
        <b-icon icon="plus-circle" variant="light" class="mx-auto my-auto icon-inter" />
        <b-card bg-variant="transparent" text-variant="white" :header="content.experienceLabel[language]" class="text-center my-3">
          <b-icon icon="briefcase-fill" variant="light" class="mx-auto my-auto icon-inside" />
        </b-card>
        <b-icon icon="plus-circle" variant="light" class="mx-auto my-auto icon-inter" />
        <b-card bg-variant="transparent" text-variant="white" :header="content.skillLabel[language]" class="text-center my-3">
          <b-icon icon="person-lines-fill" variant="light" class="mx-auto my-auto icon-inside" />
        </b-card>
        <b-icon icon="plus-circle" variant="light" class="mx-auto my-auto icon-inter" />
        <b-card bg-variant="transparent" text-variant="white" :header="content.courseLabel[language]" class="text-center my-3">
          <b-icon icon="pencil-fill" variant="light" class="mx-auto my-auto icon-inside" />
        </b-card>
        <b-icon icon="plus-circle" variant="light" class="mx-auto my-auto icon-inter" />
        <b-card bg-variant="transparent" text-variant="white" :header="content.educationLabel[language]" class="text-center my-3">
          <b-icon icon="book-half" variant="" class="mx-auto my-auto icon-inside" />
        </b-card>
      </b-card-group>
      <div class="my-3">
        <b-card-group deck>
          <b-icon icon="arrow-down-circle" variant="light" class="mx-auto my-auto icon-inter" />
        </b-card-group>
      </div>
      <div class="my-3">
        <b-card-group deck>
          <b-card bg-variant="transparent" text-variant="white" :header="content.successLabel[language]" class="text-center">
            <b-icon icon="bullseye" variant="success" class="mx-auto my-auto icon-inside" />
          </b-card>
        </b-card-group>
      </div>
      <b-button class="button-purple">
        <nuxtLink to="/Cv" class="nav-link text-white">
          {{ content.homeButton[language] }}
        </nuxtLink>
      </b-button>
    </b-container>
    <!-- Paralax -->
    <div class="parallax-home w-100" />
    <!-- Testimonial carousel for desktop -->
    <div class="testimonial-carousel w-100">
      <b-carousel
        id="carousel-fade"
        fade
        indicators
        :interval="3000"
      >
        <b-carousel-slide
          :img-src="require('../assets/people-in-computer.jpg')"
        >
          <b-card class="shadow bg-overlay">
            <b-card-body>
              <b-icon icon="chat-quote-fill" variant="light" class="icon-inter mb-3 mt-5" />
              <b-card-text class="h3 mb-5">
                {{ content.testimonialA[language] }}
              </b-card-text>
              <b-avatar :src="require('../assets/maria-lopez-testimonial.jpg')" size="6rem" />
            </b-card-body>
            <template #footer>
              <p>
                {{ content.testimonialFooterA[language] }}
              </p>
            </template>
          </b-card>
        </b-carousel-slide>
        <b-carousel-slide
          :img-src="require('../assets/people-coffee-computer.jpg')"
        >
          <b-card class="shadow bg-overlay">
            <b-card-body>
              <b-icon icon="chat-quote-fill" variant="light" class="icon-inter mb-3 mt-5" />
              <b-card-text class="h3 mb-5">
                {{ content.testimonialB[language] }}
              </b-card-text>
              <b-avatar :src="require('../assets/john-snow-testimonial.jpg')" size="6rem" />
            </b-card-body>
            <template #footer>
              <p>
                {{ content.testimonialFooterB[language] }}
              </p>
            </template>
          </b-card>
        </b-carousel-slide>
      </b-carousel>
    </div>
    <!-- Testimonial card for mobile -->
    <b-container fluid class="testimonial-card w-100">
      <b-card-group deck>
        <b-card variant="light" class="my-5">
          <b-card-body>
            <b-icon icon="chat-quote-fill" variant="dark" class="icon-inter mb-3 mt-5" />
            <b-card-text class="h3 mb-5">
              {{ content.testimonialA[language] }}
            </b-card-text>
            <b-avatar :src="require('../assets/maria-lopez-testimonial.jpg')" size="6rem" />
          </b-card-body>
          <template #footer>
            <p>
              {{ content.testimonialFooterA[language] }}
            </p>
          </template>
        </b-card>
        <b-card variant="light" class="my-5">
          <b-card-body>
            <b-icon icon="chat-quote-fill" variant="dark" class="icon-inter mb-3 mt-5" />
            <b-card-text class="h3 mb-5">
              {{ content.testimonialB[language] }}
            </b-card-text>
            <b-avatar :src="require('../assets/john-snow-testimonial.jpg')" size="6rem" />
          </b-card-body>
          <template #footer>
            <p>
              {{ content.testimonialFooterB[language] }}
            </p>
          </template>
        </b-card>
      </b-card-group>
    </b-container>
    <!-- Card with highlight -->
    <b-container fluid>
      <b-card text-variant="white" class="bg-transparent w-100">
        <template #header>
          <span class="small-title">
            {{ "CV GENERAT" }}<b-icon icon="globe" />{{ "R" }}
          </span>
        </template>
        <b-card-text>
          {{ content.homeDescription[language] }}
        </b-card-text>
        <b-button class="button-purple my-3">
          <nuxtLink to="/Cv" class="nav-link text-white">
            {{ content.homeButton[language] }}
          </nuxtLink>
        </b-button>
      </b-card>
    </b-container>
  </section>
</template>

<script>
// Export
export default {
  // Name and components
  name: 'Home',
  // Properties received from parent
  props: ['content', 'language']
}
</script>

<style scoped >

  .bg-grey-linear {
    background: linear-gradient(39deg, rgba(2,0,36,1) 67%, rgba(77,71,92,1) 90%);
  }

  .bg-overlay {
    background: linear-gradient(45deg, rgba(2,0,36,0.35423676306460083) 0%, rgba(2,0,36,0.49709390592174374) 0%);
  }

  .icon-inter {
    font-size:3rem
  }

  .icon-inside {
    font-size:5rem
  }

  .big-title {
    color:whitesmoke;
  }

  .small-title {
    color:whitesmoke;
    font-size:3rem;
  }

  .button-purple {
    background-color:#8357e5;
    border: none;
    color: whitesmoke;
    text-align: center;
    text-decoration: none;
    font-size: 16px;
    filter: brightness(75%);
    transition-delay: 0.25s;
    transition-timing-function: ease-out;
    transition: filter 1s;
  }

  .button-purple:hover {
    background-color:#8357e5;
    border: none;
    color: whitesmoke;
    text-align: center;
    text-decoration: none;
    font-size: 16px;
    filter: brightness(100%);
  }

  .parallax-home {
    /* The image used */
    background-image: url("../assets/people-brain-storm.jpg");
    /* Height */
    height: 33vh;
    /* Create the parallax scrolling effect */
    background-attachment: fixed;
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;
  }

  .testimonial-card {
    display:none;
  }

  .top-margin {
    /* Height */
    min-height: 15vh;
  }

  /* Extra small devices (phones, 600px and down) */
  @media only screen and (max-width: 600px) {
    .parallax-home {display:none;}
    .top-margin {display:none;}
    .big-title {font-size:8vw;}
    .big-sub-title {font-size:6vw;}
    .small-title {font-size:8vw;}
    .testimonial-carousel {display:none;}
    .testimonial-card {display:block;}
  }

</style>
