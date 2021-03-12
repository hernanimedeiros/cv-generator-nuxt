<template>
  <section class="simple-black d-flex justify-content-center">
    <b-container class="text-center my-auto">
      <Nuxt />
    </b-container>
  </section>
</template>

<script>
export default {
  name: 'SimpleLayout'
}
</script>

<style>
  a {
    color: green;
    text-decoration: none;
  }

  a:hover{
    color:greenyellow;
    text-decoration: none;
  }

  .simple-black {
    background: black;
    color: whitesmoke;
    height:100vh;
    width:100vw;
  }

</style>
