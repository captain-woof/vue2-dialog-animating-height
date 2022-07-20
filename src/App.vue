<script>
import Dialog from './components/Dialog.vue'
export default {
  name: 'App',
  components: {
    Dialog
  },
  data: () => ({
    carouselData: [
      {
        title: "Lorem ipsum dolor sit amet",
        description: "Proin non tristique felis. Sed porta eros quis libero mollis porta. Nam auctor diam sit amet metus bibendum tempor. Integer nibh risus, scelerisque sed ex a, sagittis tempus tortor."
      },
      {
        title: "Sed sed mattis sem",
        description: "Suspendisse eu erat quis justo pulvinar congue. Phasellus finibus consequat orci. Aliquam vitae neque quis eros fermentum suscipit. Donec semper suscipit sem at blandit."
      },
      {
        title: "Interdum et malesuada",
        description: "Morbi dapibus purus et nisi tincidunt, ut elementum est lacinia. Sed varius finibus ante vitae sodales. Nunc lacinia mauris a leo fermentum,"
      }
    ]
  })
}
</script>

<template>
  <Dialog :carouselData="carouselData" />
</template>

<style>
html,
:root {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin: 0;
}

* {
  box-sizing: border-box;
}

h1 {
  line-height: 1.5;
}

p {
  margin: 0;
  line-height: 1.25;
}

button {
  margin: 0;
  padding: 0;
  border: none;
  outline: none;
  font-family: inherit;
  display: block;
  cursor: pointer;
}
</style>
