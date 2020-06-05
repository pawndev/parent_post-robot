<template>
  <div class="container">
    <button @click="sendEventToModal">Send my event</button>
    <iframe src="https://relaxed-aryabhata-896568.netlify.app/" :name="name" />
    <div v-if="displayModal">Je suis une modale</div>
  </div>
</template>

<script>
import postRobot from 'post-robot'

const allnames = ['Boulou', 'Billy', 'Bobby', 'Tux']

export default {
  data() {
    return {
      displayModal: false,
      name: Math.random()
        .toString(36)
        .substring(7)
    }
  },
  mounted() {
    postRobot.on('display_modal', (evt) => {
      const info = evt.data
      alert(`Animal: ${info.animal}, has name: ${info.name}`)
      info.clearName()
    })
  },
  methods: {
    sendEventToModal() {
      postRobot.send(window.frames[this.name], 'fill_name', {
        name: allnames[Math.floor(Math.random() * allnames.length)],
        toggleModal: () => (this.displayModal = !this.displayModal)
      })
      return true
    }
  }
}
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
  @apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
