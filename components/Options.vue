<template>
  <section class="static-options my-5 w-100">
    <b-card
      bg-variant="light"
      class="mx-lg-5 shadow"
    >
      <b-card-body>
        <b-card-title>
          {{ content.optionsTitle[language] }}
        </b-card-title>
        <b-card-text>
          {{ content.optionsSubTitle[language] }}
        </b-card-text>
      </b-card-body>
      <!-- Stars On/Off-->
      <!-- Label -->
      <b-form-group
        :label="content.optionsLabelElement[language]"
        label-cols-lg="3"
        label-size="lg"
        label-class="font-weight-bold pt-0"
        class="mb-0"
      >
        <!-- Item -->
        <b-form-group
          :label="content.skillRatingShow[language]"
          label-cols-sm="3"
          label-align-sm="right"
          label-for="skillRatingShow"
          class="align-items-center"
        >
          <b-form-checkbox
            v-model="rating"
            name="check-button"
            switch
            class="check-box-rating"
          />
        </b-form-group>
      </b-form-group>
      <!-- Side-Wrapper configuration -->
      <!-- Label -->
      <b-form-group
        :label="content.optionsLabelColor[language]"
        label-cols-lg="3"
        label-size="lg"
        label-class="font-weight-bold pt-0"
        class="mb-0"
      >
        <!-- Background -->
        <b-form-group
          :label="content.optionsBackground[language]"
          label-cols-sm="3"
          label-align-sm="right"
          label-for="backgroundColorPicker"
        >
          <b-form-input
            id="backgroundColorPicker"
            v-model="sidebarWrapperBackground"
            placeholder="#20b2aa"
            type="color"
          />
        </b-form-group>
        <!-- Text color -->
        <b-form-group
          :label="content.optionsColor[language]"
          label-cols-sm="3"
          label-align-sm="right"
          label-for="textColorPicker"
        >
          <b-form-input
            id="textColorPicker"
            v-model="sidebarWrapperColor"
            placeholder="#ffffff"
            type="color"
          />
        </b-form-group>
      </b-form-group>
      <!-- Preview -->
      <b-card
        bg-variant="light"
        class="mx-auto shadow"
      >
        <b-card-body
          :style="{ background: sidebarWrapperBackground, color: sidebarWrapperColor }"
        >
          <b-card-title>
            {{ content.optionsExample[language] }}
          </b-card-title>
          <p>
            {{ content.loremShort[language] }}
          </p>
        </b-card-body>
      </b-card>
      <!-- Complete and incomplete state toggle -->
      <div class="mt-3 d-flex justify-content-end">
        <b-button
          id="tooltip-target-6"
          variant="outline-secondary"
        >
          <div class="d-flex justify-content-end">
            <!-- Label -->
            <span class="mr-3">
              {{ content.completedLabel[language] }}
            </span>
            <!-- Incomplete -->
            <div
              v-show="completed"
              @click="completedToogle(); incompletedToast()"
            >
              <b-icon
                icon="circle-fill"
                variant="success"
              />
            </div>
            <!-- Complete -->
            <div
              v-show="!completed"
              @click="completedToogle(); changeOptions (); completedToast()"
            >
              <b-icon
                icon="circle-fill"
                variant="outline-danger"
              />
            </div>
          </div>
        </b-button>
        <!-- Tooltip -->
        <b-tooltip target="tooltip-target-6" placement="left" triggers="hover">
          {{ content.completedInfo[language] }}
        </b-tooltip>
      </div>
    </b-card>
  </section>
</template>

<script>
// Import
// @ is an alias to /src
import { mapGetters, mapMutations } from 'vuex'
// Export
export default {
  // Name and components
  name: 'Options',
  // Properties received from parent
  props: ['content', 'language'],
  data () {
    return {
      // Default items
      completed: false,
      // Default values
      options: [
        {
          rating: true,
          sidebarWrapperBackground: '#20b2aa',
          sidebarWrapperColor: '#ffffff'
        }
      ],
      rating: true,
      sidebarWrapperBackground: '#20b2aa',
      sidebarWrapperColor: '#ffffff'
    }
  },
  computed: {
    // Shortcut to getters
    ...mapGetters({
      getOptions: 'options/get'
    })
  },
  mounted () {
    // This values are a dependecy of others modules
    this.setOptions(this.options)
  },
  methods: {
    // Shortcut to mutations
    ...mapMutations({
      setOptions: 'options/set'
    }),
    completedToogle () {
      this.completed = !(this.completed)
      return true
    },
    changeOptions () {
      this.options[0].rating = this.rating
      this.options[0].sidebarWrapperBackground = this.sidebarWrapperBackground
      this.options[0].sidebarWrapperColor = this.sidebarWrapperColor
      this.setOptions(this.options)
    },
    // Toasts
    completedToast () {
      this.$bvToast.toast(this.content.completedMessageB[this.language], {
        title: this.content.completedMessageA[this.language],
        variant: 'success',
        solid: true
      })
    },
    incompletedToast () {
      this.$bvToast.toast(this.content.incompletedMessageB[this.language], {
        title: this.content.incompletedMessageA[this.language],
        variant: 'danger',
        solid: true
      })
    }
  }
}
</script>

<style scoped>
  .check-box-rating {
    text-align: left;
  }
  @media only screen and (max-width: 600px) {
    .check-box-rating {text-align: center;}
  }
</style>
