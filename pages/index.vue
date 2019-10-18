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
            <p class="is-size-7 has-text-centered">
              Keep trying for an even spookier name!
            </p>
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
      const names = name.split(' ')
      const firstLetter = names[0].toLowerCase().substring(0, 1)
      // 1) if the first letter has a spooky word, use it
      const spookyWords = this.spookyWords(firstLetter)
      // 2) Last name + something
      const random = Math.floor(Math.random() * spookyWords.length)
      let generatedName = spookyWords[random]
      names.forEach((name) => {
        generatedName = `${generatedName} ${name}`
      })
      // 3) Add an emoji
      const emojis = ['👻', '🎃', '😱', '💀', '☠️', '🧛‍♀️', '🧛‍♂️', '🧟‍♀️', '🧟‍♂️', '🕷', '🦇']
      const randomEmoji = Math.floor(Math.random() * emojis.length)
      generatedName = `${emojis[randomEmoji]} ${generatedName} ${emojis[randomEmoji]}`
      return generatedName
    },
    spookyWords (letter) {
      switch (letter) {
        case 'a':
          return ['AHHHHH', 'Alarming', 'Axe Murdering']
        case 'b':
          return ['Beastly', 'Boo', 'Blood', 'Bloody', 'Bat']
        case 'c':
          return ['Creepy', 'Cackling']
        case 'd':
          return ['Dracula', 'Dastardly', 'Dead', 'Dreadful', 'Dreary', 'Dark']
        case 'e':
          return ['Eerie', 'Evil']
        case 'f':
          return ['Fearsome', 'Fiendish', 'Fear', 'Fright', 'Frankenstein']
        case 'g':
          return ['Gory', 'Ghost', 'Ghostly', 'Ghastly', 'Grisly', 'Gruesome', 'Ghoul', 'Ghoulish']
        case 'h':
          return ['Horrible', 'Howling', 'Haunted', 'Halloween']
        case 'i':
          return ['Icky', 'Invisible']
        case 'j':
          return ['Jugular', "Jack O'Lantern"]
        case 'k':
          return ['Killer']
        case 'l':
          return ['Lucifer']
        case 'm':
          return ['Mysterious', 'Mischievous', 'Monster', 'Mutilation', 'Morbid', 'Murder']
        case 'n':
          return ['Nightmare']
        case 'o':
          return ['Oozy', 'Ogre', 'Oooooooohhhhhhhoh']
        case 'p':
          return ['Petrifying']
        case 's':
          return ['Spooky', 'Startling', 'Spewing', 'Strange', 'Skull', 'Scary']
        default:
          return ['Spooky']
      }
    }
  }
}
</script>

<style>
</style>
