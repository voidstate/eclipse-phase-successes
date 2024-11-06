<script setup>
defineProps( {
  label: {
    type: String,
    required: true,
  },
  result: {
    type: String,
    required: false,
  },
} )
</script>

<template>
  <div class="msgs">
    <h1 class="green">{{ result }}</h1>
    <h3>
      {{ label }}
    </h3>
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2rem;
  position: relative;
}

h3 {
  font-size: 1.2rem;
  margin-bottom: 2rem;
}

.msgs h1,
.msgs h3 {
  text-align: center;
}

@media (min-width: 1024px) {

  .msgs h1,
  .msgs h3 {
    text-align: left;
  }

  section#result {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);

    .wrapper {
      display: flex;
      place-items: flex-start;
      flex-wrap: wrap;
    }
  }

}
</style>
