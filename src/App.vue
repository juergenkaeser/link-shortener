<template>
  <div class="content-wrapper">
    <div class="form-wrapper">
      <label for="url">Enter URL to shorten:</label>
      <input type="text" name="url" v-model="enteredUrl">
      <button @click="shortenUrl">Shorten & Copy</button>
    </div>
    <div class="shortenend-url" v-if="shortenedUrl.length > 0">
      Shortened URL coppied the the clipboard: {{ shortenedUrl }}
    </div>
  </div>
</template>

<script lang="ts">
  export default {
    data() {
      return {
        enteredUrl: '',
        shortenedUrl: ''
      }
    },
    methods: {
      shortenUrl: async function() {
        const response = await fetch(`https://api.shrtco.de/v2/shorten?url=${this.enteredUrl}`)
        const data = await response.json()
        if (data) {
          this.shortenedUrl = data.result.short_link          
          navigator.clipboard.writeText(this.shortenedUrl).then()
        }
      }
    }
  }
</script>

<style lang="scss" scoped>
.content-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  height: 20vh;
  padding: 24px;
  margin: auto;
  background-color: #bde0d5;
  border: 2px solid #5C6F68;
  border-radius: 8px;
  color: #1b3629;

  .form-wrapper {
    margin-bottom: 24px;
    label {
      margin-right: 8px;
      font-weight: bold;
    }
    input {
      margin-right: 8px;
    }
  }

  .shortenend-url {
    color: #1a3d29
  }
}
</style>
