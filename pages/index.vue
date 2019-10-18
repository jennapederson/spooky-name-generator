<template>
  <section class="hero is-default is-fullheight-with-navbar">
    <div class="hero-body">
      <div class="container">
        <div class="columns is-vcentered has-text-centered">
          <div class="column is-half is-offset-one-quarter">
            <h1 class="title">
              👻 Spooky Name Generator 🎃
            </h1>
            <h2 class="subtitle">
              Generate your spooky name and then add it to your Twitter account.
            </h2>
          </div>
        </div>
        <div class="columns is-vcentered">
          <div class="column is-half is-offset-one-quarter">
            <div class="field has-addons has-addons-centered">
              <div class="control">
                <input v-model="name"
                  class="input"
                  type="text"
                  placeholder="Your name"
                  @keyup.enter="generateName">
              </div>
              <div class="control">
                <a class="button is-dark"
                  :disabled="name.length == 0"
                  @click="generateName">
                  Spook it out
                </a>
              </div>
            </div>
          </div>
        </div>
        <div class="columns is-vcentered">
          <div class="column is-half is-offset-one-quarter has-text-centered">
            <p v-for="(name, index) in generatedNames" :key="`${name}-${index}`">
              {{ name }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  data: () => {
    return {
      name: '',
      generatedNames: []
    }
  },
  methods: {
    generateName () {
      const generatedName = this.generateSpookyName(this.name)
      this.generatedNames.push(generatedName)
    },
    generateSpookyName (name) {
      const firstLetter = name.toLowerCase().substring(0, 1)
      switch (firstLetter) {
        case 'a':
          return `Ahhhhh ${name}`
        case 'j':
          return `${name} o' Lantern`
        case 's':
          return `Spooky ${name}`
      }
      return `Spooky ${name}`
    }
  }
}
</script>

<style>
</style>
