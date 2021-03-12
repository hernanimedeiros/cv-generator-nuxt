<template>
  <b-navbar
    id="nav"
    toggleable="lg"
    type="dark"
    variant="dark"
    class="dinamic-nav bg-dark fixed-top justify-content-end no-printme w-100"
  >
    <!-- Logo -->
    <b-navbar-brand>
      <nuxtLink to="/" class="nav-link text-muted">
        {{ "CV GENERAT" }}<b-icon icon="globe" />{{ "R" }}
      </nuxtLink>
    </b-navbar-brand>
    <!-- Toggle to mobile -->
    <b-navbar-toggle target="nav-collapse" />
    <!-- Collapse items -->
    <b-collapse
      id="nav-collapse"
      is-nav
      class="bg-dark"
    >
      <!-- Items -->
      <b-navbar-nav class="ml-auto">
        <b-nav-item>
          <nuxtLink to="/" class="nav-link">
            <b-icon icon="house-fill" />
          </nuxtLink>
        </b-nav-item>
        <!-- Item -->
        <b-nav-item>
          <nuxtLink to="/Cv" class="nav-link">
            {{ content.navBarService[language] }}
          </nuxtLink>
        </b-nav-item>
        <!-- Item -->
        <b-nav-item>
          <nuxtLink to="/About" class="nav-link">
            {{ content.navBarAbout[language] }}
          </nuxtLink>
        </b-nav-item>
        <!-- Item -->
        <b-nav-item>
          <!-- Call help -->
          <CvHelp
            :content="content"
            :language="language"
          />
        </b-nav-item>
        <!-- Item -->
        <b-nav-item class="my-auto">
          <!-- Language change component (modal) -->
          <LanguageSet
            v-once
            :content="content"
            :language="language"
            :preferences="preferences"
          />
        </b-nav-item>
      </b-navbar-nav>
    </b-collapse>
  </b-navbar>
</template>

<script>
// Import
// @ is an alias to /src
import LanguageSet from '@/components/LanguageSet.vue'
import CvHelp from '@/components/CvHelp.vue'
// Export
export default {
  // Name and components
  name: 'DinamicNav',
  components: {
    LanguageSet,
    CvHelp
  },
  // Properties received from parent
  props: ['content', 'language', 'preferences']
}
</script>

<style scoped>
  #nav a {
    color: whitesmoke;
  }

  #nav a:hover {
    color: lightgrey;
  }

  .dinamic-nav {
    max-height: 3.5rem;
    width:100vw;
    opacity: 0.33;
    transition: opacity 1s;
  }

  .dinamic-nav:hover {
    opacity: 0.75;
  }

  .b-icon {
    color: whitesmoke;
  }

  .b-icon:hover {
    color: lightgrey;
  }
</style>
