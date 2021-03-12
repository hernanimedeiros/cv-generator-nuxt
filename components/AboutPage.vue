<template>
  <section class="about-page bg-grey-linear w-100">
    <!-- Navigation -->
    <b-container>
      <nuxtLink to="/">
        <b-icon class="floating-button-side-a shadow-lg" icon="house-fill" variant="light" />
      </nuxtLink>
      <nuxtLink to="/Cv">
        <b-icon class="floating-button-side-b shadow-lg" icon="file-earmark" variant="light" />
      </nuxtLink>
    </b-container>
    <!-- Welcome screen  -->
    <b-container fluid class="bg-about w-100 h-100">
      <b-row>
        <!-- Cv -->
        <b-col lg="6" class="text-white h-100 bg-overlay">
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
            <p class="p-one-half">
              {{ content.homeDescription[language] }}
            </p>
            <b-button class="outline-dark bg-transparent border-white button-edge">
              <nuxtLink to="/Cv" class="text-white">
                {{ content.homeButton[language] }}
              </nuxtLink>
            </b-button>
          </b-jumbotron>
        </b-col>
        <!-- About -->
        <b-col lg="6" class="text-white h-100 bg-no">
          <b-jumbotron class="bg-transparent" text-variant="white">
            <template #header>
              <span class="big-title">
                {{ content.aboutTitle[language] }}
              </span>
            </template>
            <b-button href="#aboutId" class="bg-transparent border-0 b-icon-down">
              <b-icon icon="arrow-down-circle" scale="2" />
            </b-button>
            <p class="p-one-half">
              {{ content.aboutSubTitle[language] }}
            </p>
          </b-jumbotron>
        </b-col>
      </b-row>
    </b-container>
    <!-- Main  -->
    <b-container id="aboutId" fluid class="w-100 my-5">
      <b-row>
        <b-col lg="3" class="text-white my-5">
          <a href="https://www.facebook.com/hernanifelixmedeiros/" target="_blank">
            <i class="fab fa-facebook-square icon-link icon-facebook" />
          </a>
        </b-col>
        <b-col lg="3" class="text-white my-5">
          <a href="https://api.whatsapp.com/send?phone=351915531511&text=Deixe-nos%20a%20sua%20mensagem.%20Obrigado%20pela%20prefer%C3%AAncia" target="_blank">
            <i class="fab fa-whatsapp icon-link icon-whatsapp" />
          </a>
        </b-col>
        <b-col lg="3" class="text-white my-5">
          <a href="mailto:hernanimedeiros@hotmail.com?Subject=CvGenerator%20contato" target="_blank">
            <i class="fas fa-at icon-link icon-mail" />
          </a>
        </b-col>
        <b-col lg="3" class="text-white my-5">
          <a href="https://www.linkedin.com/in/hernanimedeiros/" target="_blank">
            <i class="fab fa-linkedin icon-link icon-linkedin" />
          </a>
        </b-col>
      </b-row>
    </b-container>
    <!-- Card with highlight -->
    <b-container fluid class="w-100">
      <b-card text-variant="white" class="bg-transparent w-100">
        <template #header>
          <span class="small-title">
            {{ "CV GENERAT" }}<b-icon icon="globe" />{{ "R" }}
          </span>
        </template>
        <b-card-text>
          <p> {{ content.lorem[language] }} </p>
          <p> {{ content.lorem[language] }} </p>
        </b-card-text>
        <b-button href="https://forms.gle/buCrfJcTKjqiPCseA" target="_blank" class="outline-dark bg-transparent border-white button-edge my-3">
          {{ content.aboutButton[language] }}
        </b-button>
      </b-card>
    </b-container>
  </section>
</template>

<script>
export default {
// Name and components
  name: 'AboutPage',
  // Parameters received by parent
  props: ['content', 'language']

}
</script>

<style scoped>

  a:hover{
    text-decoration: none;
  }

  .b-icon-down {
    transition-delay: 1s;
    transition-timing-function: ease-in-out;
    transition: transform 1s;
  }

  .b-icon-down:hover {
    transform: translateY(10%);
  }

  .big-title {
    color:whitesmoke;
    text-shadow: 5px 5px 10px black;
  }

  .bg-grey-linear {
    background: linear-gradient(39deg, rgba(2,0,36,1) 67%, rgba(77,71,92,1) 90%);
    min-height: 100vh;
  }

  .bg-overlay {
    background: linear-gradient(45deg, rgba(2,0,36,0.35423676306460083) 0%, rgba(2,0,36,0.49709390592174374) 0%);
    min-height: 100vh;
  }

  .bg-about {
    background-image: url("../assets/cv-generator-team-working.jpg");
    height: 100vh;
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;
  }

  .button-edge {
    font-size:1rem;
    transition-delay: 1s;
    transition-timing-function: ease-out;
    transition: transform 1s;
  }

  .button-edge:hover {
    transform: scale(1.1);
  }

  .icon-link {
    font-size:5rem;
    filter: grayscale(100%);
    transition-delay: 1s;
    transition-timing-function: ease-in-out;
    transition: transform 3s, filter 3s;
  }

  .icon-link:hover {
    transform: scale(1.5);
    filter: grayscale(0%);
  }

  .icon-facebook {
    color: #3974e7;
  }

  .icon-linkedin {
    color: #3066C2;
  }

  .icon-mail {
    color: #8357e5;
  }

  .icon-whatsapp {
    color: #57E676;
  }

  .icons {
    font-size:2rem;
    text-shadow: 5px 5px 10px black;
  }

  .floating-button-side-a {
    position: fixed;
    top: 45vh;
    left: 0.5rem;
    font-size: 2rem;
    opacity: 0.25;
    border-radius: 50%;
    z-index: 2;
    transition-delay: 1s;
    transition-timing-function: ease-out;
    transition: transform 0.4s, opacity 1s;
  }

  .floating-button-side-a:hover {
    transform: scale(1.5);
    opacity: 1;
  }

  .floating-button-side-b {
    position: fixed;
    top: 55vh;
    left: 0.5rem;
    font-size: 2rem;
    opacity: 0.25;
    border-radius: 50%;
    z-index: 2;
    transition-delay: 0.25s;
    transition-timing-function: ease-out;
    transition: transform 0.4s, opacity 1s;
  }

  .floating-button-side-b:hover {
    transform: scale(1.5);
    opacity: 1;
  }

  .p-one-half {
    font-size:1.5rem;
    text-shadow: 5px 5px 10px black;
  }

  .small-title {
    color:whitesmoke;
    font-size:3rem;
  }

  .top-margin {
    /* Height */
    min-height: 15vh;
  }

  /* Extra small devices (phones, 600px and down) */
  @media only screen and (max-width: 600px) {
    .bg-grey-linear {min-height: 50vh;}
    .bg-overlay {min-height: 50vh;}
    .bg-no {min-height: 50vh;}
    .big-title {font-size:8vw;}
    .big-sub-title {font-size:6vw;}
    .icon-link {font-size:25vh;filter:grayscale(0%);}
    .floating-button-side-a {top:0.5rem;left:70vw}
    .floating-button-side-b {top:0.5rem;left:85vw}
    .small-title {font-size:8vw;}
  }

</style>
