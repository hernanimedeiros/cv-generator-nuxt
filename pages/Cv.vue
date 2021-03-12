<template>
  <section>
    <section class="cv no-printme w-100">
      <div class="parallax-cv w-100" />
      <Preview :language="checkLanguage" :content="content" />
      <div class="parallax-cv mt-5 w-100" />
      <CvForm :language="checkLanguage" :content="content" />
      <Options :language="checkLanguage" :content="content" />
      <Static :language="checkLanguage" :content="content" />
      <PreviewData id="finishId" :language="checkLanguage" :content="content" />
    </section>
    <aside class="printme">
      <Pdf :language="checkLanguage" :content="content" />
    </aside>
  </section>
</template>

<script>
// Import
// @ is an alias to /src
import { mapGetters } from 'vuex'
import ContentJson from '@/content.json'
import CvForm from '@/components/CvForm.vue'
import Options from '@/components/Options.vue'
import Preview from '@/components/Preview.vue'
import PreviewData from '@/components/PreviewData.vue'
import Pdf from '@/components/Pdf.vue'
import Static from '@/components/Static.vue'
// Export
export default {
  // Name and components
  name: 'Cv',
  components: {
    CvForm,
    Options,
    Pdf,
    Preview,
    PreviewData,
    Static
  },
  data () {
    return {
      content: ContentJson
    }
  },

  // Watch store
  computed: {
    ...mapGetters({
      getPreferences: 'preferences/get'
    }),
    checkLanguage () {
      // Check current language, force 'pt' if dont come of index
      try {
        const currentLanguage = this.getPreferences[0].language
        return currentLanguage
      } catch (e) {
        return 'pt'
      }
    }
  },
  head () {
    return {
      htmlAttrs: {
        lang: this.checkLanguage
      },
      title: this.content.metaCvTitle[this.checkLanguage],
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: this.content.metaCvDescription[this.checkLanguage]
        },
        {
          hid: 'keywords',
          name: 'keywords',
          content: this.content.metaCvKeyword[this.checkLanguage]
        }
      ]
    }
  }
}
</script>

<style>

  .parallax-cv {
    /* The image used */
    background-image: url("../assets/people-brain-storm.jpg");
    /* Height */
    height: 20vh;
    /* Create the parallax scrolling effect */
    background-attachment: fixed;
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;
  }

  .printme {
      display: none;
  }

  /* Extra small devices (phones, 600px and down) */
  @media only screen and (max-width: 600px) {
    .parallax-cv {display:none;}
  }

  @media print {
    b-container::before {
      margin:0px;
      padding:0px;
    }

    #header, #nav, .no-printme  {
      display: none;
    }

    .printme  {
      display: block;
      left: 0px;
      top: 0px;
      position:absolute;
    }

  }
</style>
