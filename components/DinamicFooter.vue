<template>
  <footer class="footer text-center no-printme shadow w-100">
    <!-- Bottom alert -->
    <b-alert
      v-model="showCookiesMessage"
      class="position-fixed fixed-bottom m-0 rounded-0"
      style="z-index: 2000;"
      variant="warning"
      dismissible
    >
      {{ content.cookiesMessage[language] }}
    </b-alert>
    <!-- Footer -->
    <b-container fluid class="bg-footer w-100">
      <b-icon
        variant="dark"
        icon="arrow-up-circle-fill"
        animation="cylon-vertical"
        @click="scrollToTop"
      />
      <small>
        {{ content.authorMessageA[language] }}
        <b-icon icon="heart-fill" animation="throb" font-scale="1" variant="success" />
        <a :href="content.authorLink[language]" target="_blank">
          {{ content.authorCredit[language] }}
        </a>
        <span class="expendable-footer-part">
          {{ content.authorMessageB[language] }}
        </span>
      </small>
      <b-icon
        variant="dark"
        icon="arrow-up-circle-fill"
        animation="cylon-vertical"
        @click="scrollToTop"
      />
    </b-container>
  </footer>
</template>

<script>
// Export
export default {
  // Name and components
  name: 'DinamicFooter',
  // Properties received from parent
  props: ['content', 'language'],
  data () {
    return {
      // Load content
      showCookiesMessage: true
    }
  },
  methods: {
    scrollToTop () {
      window.scrollTo(0, 0)
    }
  }
}
</script>

<style scoped >
  a {
    font-weight: 700;
    text-decoration: none;
    color:darkgreen
  }

  a:hover {
    text-decoration: none;
    color: green;
    -webkit-transition: all 0.4s ease-in-out;
    -moz-transition: all 0.4s ease-in-out;
    -ms-transition: all 0.4s ease-in-out;
    -o-transition: all 0.4s ease-in-out;
  }

  a:focus {
    text-decoration: none;
    color:grey
  }

  .bg-footer {
    background-color:lightgray;
  }

  small:hover{
    text-decoration: none;
  }

  /* Extra small devices (phones, 600px and down) */
  @media only screen and (max-width: 600px) {
    .expendable-footer-part {display:none;}
    .bg-footer {padding-left:0;padding-right:0;}
  }
</style>
