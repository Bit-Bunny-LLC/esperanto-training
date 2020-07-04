<template>
  <b-container role="main">

    <b-row>
      <b-col>
        <h1>
          Alphabet Practice
        </h1>
      </b-col>
    </b-row>

    <b-row>
      <b-col md="8">
        <div id="letter" class="letter rounded-lg">
          {{combinedLetter}}
        </div>
      </b-col>
      <b-col md="4">
        <p>Practice the pronunciation the letter you see.</p>

        <p>Listen to an example pronunciation:</p>
        <b-button class="mr-1 mb-1">Hear
          <b-icon icon="soundwave"></b-icon>
        </b-button>

        <p>Cycle through the letters:</p>
        <b-button-toolbar>
          <b-button-group class="mr-1">
            <b-button v-on:click="prevLetter" v-b-tooltip.hover title="Previous Letter">
              <b-icon icon="chevron-bar-left"></b-icon>
            </b-button>
            <b-button v-on:click="nextLetter" v-b-tooltip.hover title="Next Letter">
              <b-icon icon="chevron-bar-right"></b-icon>
            </b-button>
            <b-button v-on:click="randLetter" v-b-tooltip.hover title="Random Letter">
              <b-icon icon="question"></b-icon>
            </b-button>
          </b-button-group>
        </b-button-toolbar>

      </b-col>
    </b-row>

  </b-container>

</template>

<style scoped>

  .letter {
    background-color: skyblue;
    padding: 2rem;
    text-align: center;
    font-size: 10rem;
    font-weight: bold;
  }

</style>

<script>

  function combinedLetter(alphabet, index) {
    return alphabet[index].majuscule + ' ' + alphabet[index].minuscule;
  }

  export default {
    layout: 'site',
    data() {
      return {
        alphabet: [],
        letterId: 0,
        combinedLetter: ''
      }
    },
    async fetch() {
      this.alphabet = await this.$http.$get('/json/alphabet.json');
      this.combinedLetter = combinedLetter(this.alphabet, this.letterId);
    },
    methods: {
      nextLetter() {
        this.letterId = this.letterId + 1;
        if (this.letterId > this.alphabet.length - 1) {
          this.letterId = 0;
        }
        this.combinedLetter = combinedLetter(this.alphabet, this.letterId);
      },
      prevLetter() {
        this.letterId = this.letterId - 1;
        if (this.letterId < 0) {
          this.letterId = this.alphabet.length - 1;
        }
        this.combinedLetter = combinedLetter(this.alphabet, this.letterId);
      },
      randLetter() {
        let newLetterId = this.letterId;
        while (newLetterId === this.letterId) {
          newLetterId = Math.floor(Math.random() * this.alphabet.length);
        }
        this.letterId = newLetterId;
        this.combinedLetter = combinedLetter(this.alphabet, this.letterId);
      }
    }
  }
</script>
