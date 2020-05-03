<template>
  <div>
    <img v-bind:src="character.image" v-bind:alt="character.name" v-bind:title="character.name">
    <h1>{{ character.name }}</h1>
    <button>Ver mas</button>
  </div>
</template>

<script>
export default {
  props: ["character"]
};
</script>
