<script setup>
import Result from './components/Result.vue'
import Controls from './components/Controls.vue'
</script>

<template>
  <header>
    <div class="logo">
      <img alt="Eclipse Phase Successes" class="logo" src="./assets/logo_white_sm.webp" height="100" />
    </div>
  </header>

  <main id="interface">
    <section id="result">
      <div class="wrapper">
        <Result label="Click the button or drag the sliders to calculate successes" :result="resultMessage" />
      </div>
    </section>

    <section id="controls">
      <Controls @result-message="updateResult" />
    </section>
  </main>

  <footer>Eclipse Phase dice roller by <a href="mailto:rpg@voidstate.com">voidstate</a> | <a href=""></a></footer>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

footer {
  padding-top: 3rem;
  text-align: center;
  font-size: 85%;
  color: var(--color-text);
}
</style>

<script>
export default {
  data()
  {
    return {
      resultMessage: '',
    }
  },
  methods: {
    updateResult: function ( value )
    {
      this.resultMessage = value
    },
  },
}
</script>
