<template>
  <section class="cvhelp">
    <!-- Button to sidebar -->
    <b-button v-b-toggle href="#example-sidebar" @click.prevent>
      {{ content.cvHelpTitle[language] }}
    </b-button>
    <!-- Button to content -->
    <b-sidebar
      id="example-sidebar"
      :title="content.cvHelpTitle[language]"
      shadow
      bg-variant="dark"
      text-variant="white"
    >
      <div class="px-3 py-2">
        <p> {{ content.cvHelpContent[language] }} </p>
        <p> {{ content.lorem[language] }} </p>
      </div>
    </b-sidebar>
  </section>
</template>

<script>
// Export
export default {
  // Name and components
  name: 'CvHelp',
  // Properties received from parent
  props: ['content', 'language', 'preferences']
}
</script>

<style>
</style>
