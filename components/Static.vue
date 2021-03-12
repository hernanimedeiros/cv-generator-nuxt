<template>
  <section class="static my-5 w-100">
    <div>
      <!-- Preview in modal -->
      <span>
        <b-icon
          v-show="sideIcon"
          v-b-tooltip.hover
          :title="content.previewBox[language]"
          variant="info"
          icon="eye-fill"
          class="floating-button"
          @click="checkCompleted(); modalShow = !modalShow"
        />
      </span>
      <b-modal
        ref="my-modal"
        v-model="modalShow"
        size="xl"
        hide-footer
        class="no-printme my-3"
      >
        <div>
          <!-- Bind elements -->
          <StaticItem
            :language="language"
            :content="content"
          />
        </div>
        <span class="my-3">
          <b-button
            variant="info"
            class="mx-auto"
            @click="printAfterModal"
          >
            {{ content.previewPdf[language] }}
          </b-button>
        </span>
      </b-modal>
    </div>
    <b-card
      bg-variant="light"
      class="mx-lg-5 shadow"
    >
      <!-- Label -->
      <b-card-body>
        <b-card-title>
          {{ content.previewTitle[language] }}
        </b-card-title>
        <b-card-text>
          {{ content.previewSubTitle[language] }}
        </b-card-text>
      </b-card-body>
      <!-- Preview in real time -->
      <div class="accordion" role="tablist">
        <b-card no-body>
          <b-card-header header-tag="header" role="tab">
            <b-button
              v-b-toggle.accordion-1
              variant="success"
            >
              {{ content.previewPage[language] }}
            </b-button>
          </b-card-header>
          <b-collapse
            id="accordion-1"
            accordion="my-accordion"
            role="tabpanel"
          >
            <b-card-body>
              <!-- Bind elements -->
              <StaticItem
                :language="language"
                :content="content"
              />
            </b-card-body>
          </b-collapse>
        </b-card>
      </div>
      <div class="mx-auto my-3">
        <!-- Save to .pdf -->
        <b-button
          variant="success"
          @click="print(), checkCompleted()"
        >
          {{ content.previewPdf[language] }}
        </b-button>
        <b-alert
          v-model="printMessage"
          class="position-fixed fixed-bottom m-0 rounded-0"
          style="z-index: 2000;"
          variant="warning"
          dismissible
        >
          {{ content.previewPdfMessage[language] }}
        </b-alert>
      </div>
    </b-card>
  </section>
</template>

<script>
// Import
import StaticItem from '@/components/StaticItem.vue'
import { mapGetters } from 'vuex'
// Export
export default {
  // Name and components
  name: 'Static',
  components: {
    StaticItem
  },
  // Properties received from parent
  props: {
    content: Object,
    language: String
  },
  data () {
    return {
      // Default items
      modalShow: false,
      printMessage: false,
      sideIcon: false
    }
  },
  computed: {
    // Shortcut to mutations
    ...mapGetters({
      getProfile: 'profile/get',
      getSkill: 'skill/get',
      getExperience: 'experience/get',
      getEducation: 'education/get',
      getCourse: 'course/get'
    })
  },
  mounted () {
    window.addEventListener('scroll', this.sideIconShow)
  },
  methods: {
    // Methods for actions
    print () {
      window.print()
    },
    closeModal () {
      this.$refs['my-modal'].hide()
    },
    printAfterModal () {
      this.closeModal()
      setTimeout(this.print, 1000)
    },
    printMessageShow () {
      this.printMessage = true
    },
    sideIconShow () {
      this.sideIcon = true
    },
    checkCompleted () {
      try {
        if (this.getProfile[0].profileCompleted &&
        this.getSkill[0].skillCompleted &&
        this.getExperience[0].experienceCompleted &&
        this.getEducation[0].educationCompleted &&
        this.getCourse[0].courseCompleted) {
          setTimeout(this.completedItemsToast, 1000)
        } else {
          setTimeout(this.incompletedItemsToast, 3000)
        }
      } catch (e) {
        setTimeout(this.incompletedItemsToast, 3000)
      } finally {
        setTimeout(this.printMessageShow, 1000)
      }
    },
    incompletedItemsToast () {
      this.$bvToast.toast(this.content.incompletedMessageC[this.language], {
        title: this.content.incompletedMessageA[this.language],
        variant: 'danger',
        solid: true
      })
    },
    completedItemsToast () {
      this.$bvToast.toast(this.content.completedMessageC[this.language], {
        title: this.content.completedMessageA[this.language],
        variant: 'success',
        solid: true
      })
    }
  }
}
</script>

<style scoped>
  .floating-button {
    position: fixed;
    top: 50vh;
    left: 0.5rem;
    font-size: 2rem;
    opacity: 0;
    border-radius: 50%;
    z-index: 2;
    animation-name: floating-button-anim;
    animation-delay: 5s;
    animation-duration: 10s;
    animation-iteration-count:infinite;
    animation-timing-function: ease-in-out;
  }

  @keyframes floating-button-anim{
    0%  {opacity:0}
    25% {opacity:0.33}
    50% {opacity:0.66}
    75% {opacity:0.33}
    100% {opacity:0.0}
  }

  /* Extra small devices (phones, 600px and down) */
  @media only screen and (max-width: 600px) {
    .floating-button {display:none;}
  }
</style>
