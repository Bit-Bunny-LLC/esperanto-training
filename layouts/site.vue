<template>
  <div>
    <b-navbar toggleable="md" type="dark" variant="dark">
      <b-navbar-brand :href="localePath('/')">Esperanto Training</b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav class="ml-auto">
          <b-nav-item-dropdown :text="currentLocale" right>
            <b-dropdown-item v-for="locale in availableLocales" v-bind:key="locale.key"
                             v-on:click="changeLocale(locale.code)">{{locale.name}}
            </b-dropdown-item>
          </b-nav-item-dropdown>
        </b-navbar-nav>
      </b-collapse>

    </b-navbar>

    <Nuxt/>

    <Footer/>

  </div>
</template>

<style>
  .navbar {
    margin-bottom: 2rem;
  }
</style>

<script>
  import {setLocaleCookie} from "../.nuxt/nuxt-i18n/utils-common";

  export default {
    computed: {
      currentLocale() {
        return this.$i18n.locales.filter(i => i.code === this.$i18n.locale)[0].name
      },
      availableLocales() {
        return this.$i18n.locales.filter(i => i.code !== this.$i18n.locale)
      }
    },
    methods: {
      changeLocale(code) {
        console.log(code);
        this.$i18n.setLocaleCookie(code);
        this.$router.push(this.switchLocalePath(code));
      }
    }
  }
</script>
