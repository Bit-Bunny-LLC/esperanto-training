<template>
  <div>
    <main role="main" class="container">

      <b-jumbotron header="Esperanto Training" style="margin-top:2rem;">
        <p>Useful tools for learning and practicing Esperanto, the universal language.</p>
      </b-jumbotron>

      <div class="container">
        <!-- Example row of columns -->
        <div class="row">
          <div class="col-md-4">
            <h2>Alphabet</h2>
            <p>Learn and practice pronouncing the alphabet.</p>

            <b-button-toolbar>
              <b-button-group class="mr-1 mb-1">
                <b-button href="/alphabet">Reference</b-button>
              </b-button-group>
              <b-button-group class="mr-1 mb-1">
                <b-button href="/alphabet" variant="primary">Practice <b-icon icon="chevron-double-right"></b-icon></b-button>
              </b-button-group>
            </b-button-toolbar>
          </div>
        </div>


      </div>

    </main>
  </div>
</template>

<script>
  export default {}
</script>
