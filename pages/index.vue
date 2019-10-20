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
      const generatedWord = spookyWords[random]

      // 3) Determine location
      const randomLocation = Math.floor(Math.random() * names.length + 1) - 1
      let generatedName = ''
      names.forEach((name, index) => {
        if (index === randomLocation) {
          generatedName = `${generatedName} ${generatedWord} ${name}`
        } else {
          generatedName = `${generatedName} ${name}`
        }
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
          return ['Beastly', 'Boo', 'Blood', 'Bloody', 'Bat', 'Batty']
        case 'c':
          return ['Creepy', 'Cackling', 'Chiller', 'Creepy Crawly']
        case 'd':
          return ['Dracula', 'Dastardly', 'Dead', 'Dreadful', 'Dreary', 'Dark']
        case 'e':
          return ['Eerie', 'Evil', 'Eyeballs']
        case 'f':
          return ['Fearsome', 'Fiendish', 'Fear', 'Fright', 'Frankenstein', 'Freaky']
        case 'g':
          return ['Gory', 'Ghost', 'Ghosty', 'Ghostly', 'Ghastly', 'Grisly', 'Gruesome', 'Ghoul', 'Ghoulish', 'Goblin']
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
          return ['Mysterious', 'Mischievous', 'Monster', 'Mutilation', 'Morbid', 'Murder', 'Mummy']
        case 'n':
          return ['Nightmare']
        case 'o':
          return ['Oozy', 'Ogre', 'Oooooooohhhhhhhoh']
        case 'p':
          return ['Petrifying', 'Pumpkin']
        case 'q':
          return ['Quivering']
        case 'r':
          return ['Rachet', 'RIP', 'Revolting']
        case 's':
          return ['Spooky', 'Spectre', 'Startling', 'Spewing', 'Strange', 'Skull', 'Scary', 'Screamer', 'Screaming', 'Scardedypants']
        case 't':
          return ['Trick or Treat', 'Terrifying', 'Tombstone']
        case 'u':
          return ['Unnerving']
        case 'v':
          return ['Vampire', 'Volatile']
        case 'w':
          return ['Wailing', 'Wraith', 'Wicked', 'Witch', 'Witchy', 'Witchling', 'Withering', 'Weird', 'Wolf']
        case 'x':
        case 'y':
          return ['Yowling']
        case 'z':
          return ['Zombie']
        default:
          return ['Spooky', 'Wicked', 'RIP', 'Ghostly']
      }
    }
  }
}
</script>

<style>
</style>
