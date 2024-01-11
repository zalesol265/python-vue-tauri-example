<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
  </header>

  <main>
    <TheWelcome />
    <!-- Access the pre-bundled global API functions -->
    <button @click="invokeGreet">Invoke Greet</button>

    <!-- Display the response -->
    <p>{{ greetResponse }}</p>
  </main>
</template>

<script>
export default {
  data() {
    return {
      greetResponse: null,
    };
  },
  methods: {
    async invokeGreet() {
      try {

        const response = await window.__TAURI__.tauri.invoke('greet', { name: 'World' });

        this.greetResponse = response;
      } catch (error) {
        console.error('Error invoking greet:', error);
      }
    },
  },
};
</script>


<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
