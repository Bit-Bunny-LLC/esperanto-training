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
        <p>Pronounce the letter you see.</p>

        <p>Hear a pronuciation of the letter:</p>
        <b-button class="mr-1 mb-1">Hear
          <b-icon icon="soundwave"></b-icon>
        </b-button>


        <p>Cycle through the letters:</p>
        <b-button-toolbar>
          <b-button-group class="mr-1">
            <b-button v-on:click="prevLetter">
              <b-icon icon="chevron-bar-left"></b-icon>
            </b-button>
            <b-button v-on:click="nextLetter">
              <b-icon icon="chevron-bar-right"></b-icon>
            </b-button>
            <b-button v-on:click="randLetter">
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
  export default {
    layout: 'site',
    data() {
      return {
        alphabet: [],
        letterId: 0
      }
    },
    computed: {
      combinedLetter: function () {
        return this.alphabet[this.letterId].majuscule + ' ' + this.alphabet[this.letterId].minuscule;
      }
    },
    async fetch() {
      this.alphabet = await this.$http.$get('/json/alphabet.json');
    },
    methods: {
      nextLetter() {
        this.letterId = this.letterId + 1;
        if (this.letterId > this.alphabet.length - 1) {
          this.letterId = 0;
        }
      },
      prevLetter() {
        this.letterId = this.letterId - 1;
        if (this.letterId < 0) {
          this.letterId = this.alphabet.length - 1;
        }
      },
      randLetter() {
        let newLetterId = this.letterId;
        while (newLetterId === this.letterId) {
          newLetterId = Math.floor(Math.random() * this.alphabet.length);
        }
        this.letterId = newLetterId;
      }
    }
  }
</script>
