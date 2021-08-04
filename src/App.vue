<template>
  <div class="container">
    <ListItem />
  </div>
</template>

<script>
import ListItem from "./components/ListItem.vue";

export default {
  name: "App",
  components: {
    ListItem,
  },
};
</script>

<style lang="scss">

*,
*::before,
*::after {
  box-sizing: border-box;
}

:root {
  --primary-color: #e5e7eb;
  --secondary-color: #f3f4f6;
  --third-color: #d1d5db;
  --primary-text-color: black;
  --secondary-text-color: gray;
  --item-done-color: #9ca3af;
  --btn-bg-color: rgb(219, 222, 227);
  --btn-bg-darken-color: rgb(205, 209, 216);
  --focus-border: red;

  --px: 1em;
  --py: 1em;
}

body {
  background-color: var(--secondary-color);
  font-size: 16px;
  margin: 0;
  padding-bottom: 3em;
}

/* css Utilits */
.shadow-md {
  box-shadow: 0 8px 20px rgb(17, 24, 39, 0.15);
}

.rounded-top {
  border-top-left-radius: 8px;
  border-top-right-radius: 8px;
}

.rounded-bottom {
  border-bottom-right-radius: 8px;
  border-bottom-left-radius: 8px;
}

.py-10 {
  padding-top: var(--py);
  padding-bottom: var(--py);
}

.px-10 {
  padding-right: var(--px);
  padding-left: var(--px);
}

.mt-1 {
  margin-top: 1em;
}

.mt-3 {
  margin-top: 3em;
}

.mx-center {
  margin-left: auto;
  margin-right: auto;
}

.cursor-pointer {
  cursor: pointer;
}

.d-none {
  display: none;
}

/* component */

.container {
  padding-right: 20px;
  padding-left: 20px;
  margin-right: auto;
  margin-left: auto;
}

@media (min-width: 768px) {
  .container {
    width: 600px;
  }
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  // text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
