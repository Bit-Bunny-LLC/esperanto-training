<template>
  <main role="main" class="container">

    <h1 class="title">
      Alphabet
    </h1>

    <p>Esperanto is written in a Latin-script alphabet of twenty-eight letters, with upper and lower case. This is
      supplemented by punctuation marks and by various logograms, such as the digits 0–9, currency signs such as $, and
      mathematical symbols. See the <a href="https://en.wikipedia.org/wiki/Esperanto_orthography"
                                               target="_blank" class="offsite">Esperanto Orthography
        <b-icon icon="box-arrow-up-right"></b-icon></a> article on Wikipedia for more detailed information.
    </p>

    <div>
      <b-table striped borderless small :items="items" :fields="fields">
        <template v-slot:cell(type)="data">
          <span class="type">{{data.value}}</span>
        </template>
        <template v-slot:cell(example)="data">
          <span v-html="data.value"></span>
        </template>
      </b-table>
    </div>

  </main>
</template>

<style>

  td > span.type {
    text-transform: capitalize;
  }

  em {
    font-style: normal;
    font-weight: bold;
    text-decoration: underline;
  }

  .offsite {
    white-space: nowrap;
  }

</style>

<script>
  export default {
    layout: 'site',

    data() {
      return {
        fields: [
          {key: 'type'},
          {key: 'letter', label: 'Symbol'},
          {key: 'pronounce'},
          {key: 'english', label: 'English Sound'},
          {key: 'example', label: 'English Example'}
        ],
        items: []
      }
    },
    async fetch() {
      // Create reference instance
      const marked = require('markdown-it');
      let data = await this.$http.$get('/json/alphabet.json');
      let newData = [];
      data.forEach(function (e) {
        let singleObj = {};
        singleObj.type = e.type;
        singleObj.letter = e.majuscule;
        singleObj.pronounce = e.pronunciation;
        let english = e.translations[0];
        singleObj.english = english.minuscule;
        singleObj.example = marked().renderInline(english.example);
        newData.push(singleObj);
      })
      this.items = newData;
    }
  }

</script>

