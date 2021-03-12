<template>
  <section class="w-100">
    <h1 v-if="error.statusCode === 404">
      Page not found
    </h1>
    <h1 v-else>
      An error occurred
    </h1>
    <NuxtLink to="/">
      Return to Home Page
    </NuxtLink>
  </section>
</template>

<script>
export default {
  props: ['error'],
  layout (context) {
    return 'simple'
  }
}
</script>
