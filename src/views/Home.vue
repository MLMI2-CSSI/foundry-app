<template>
  <div class="home col-12 mb-5">
    <!-- heading content -->
    <v-sheet class="text-center py-10 col-12 py-12" color="indigo lighten-2" elevation="12">
      <h1 class="text-h2 col-sm-10 col-12 mx-auto white--text pt-12">
        An open source machine learning platform for scientists
      </h1>
      <v-sheet rounded="xl" elevation="20" class="col-md-6 col-11 mx-auto mt-5 py-1">
        <p class="text-subtitle-1 col-12 my-0 mx-auto indigo--text text--lighten-2 font-weight-medium">
          Access datasets and ML models while setting industry benchmarks
        </p>
      </v-sheet>
      <h1 class="text-h2 col-10 mx-auto white--text pb-12">
      </h1>
    </v-sheet>

    <!-- middle content -->
    <v-row class="col-md-8 mx-auto col-12 mt-5 mb-8">
      <v-card elevation="3" outlined class="mx-auto col-md-5 col-12 my-6 text-center">
        <a href="#/datasets" class="text-decoration-none">
          <h1 class="display-2"><i class="mdi mdi-archive-search red--text text--lighten-3"></i></h1>

          <v-card-title class="justify-center grey--text text--darken-4">Browse Datasets</v-card-title>
          <v-card-text class="grey--text text--darken-1">
            Find the data you're looking for. See all the Foundry datasets and get started.
          </v-card-text>
        </a>
      </v-card>
      <v-card elevation="3" outlined class="mx-auto col-md-5 col-12 my-6 text-center">
        <a href="https://ai-materials-and-chemistry.gitbook.io/foundry/publishing/publishing-datasets" target="blank"
          class="text-decoration-none">
          <h1 class="display-2"><i class="mdi mdi-chart-bar-stacked red--text text--lighten-3"></i></h1>

          <v-card-title class="justify-center grey--text text--darken-4">Add your dataset</v-card-title>
          <v-card-text class="grey--text text--darken-1">
            We host data from a variety of scientific domains and make it easy to share and use.
          </v-card-text>
        </a>
      </v-card>
    </v-row>


    <!-- Starter code and metadata section -->
    <v-row class="indigo lighten-4 pt-3 px-md-10 px-1">
      <h1 class="col-md-10 col-12 mx-auto">We make collaboration and reuse easy</h1>
      <v-row class="mb-5 col-md-10 col-12 mx-auto">
        <div class="col-sm-10 col-md-6 col-12 mx-auto overflow-x-hidden scroll-fix">
          <vue-code-highlight language="python" class="overflow-x-hidden scroll-fix">
            <pre class="overflow-x-hidden language-python scroll-fix">

f = f.load("foundry_stan_segmentation_v1.1")
X,y = f.load_data()
</pre>
          </vue-code-highlight>
          <v-sheet rounded color="white" elevation="20">
            <img alt="dendrite segmentation data snippet" src="../assets/dendrite-seg-img.png" class="col-12 pb-3" />
          </v-sheet>
        </div>
        <div class="col-sm-10 col-md-6 col-12 mx-auto">
          <p>
            Once a dataset is uploaded to Foundry, you can load it with just 2
            lines of code.
          </p>
          <a class="text-decoration-none"
            href="https://colab.research.google.com/github/MLMI2-CSSI/foundry/blob/main/examples/dendrite-segmentation/dendrite_segmentation.ipynb"
            target="blank">
            <v-btn color="red lighten-2 white--text col-12 col-md-10 col-lg-8">
              Run this in Google Colab
            </v-btn>
          </a>
        </div>
      </v-row>
    </v-row>
    <!-- end of row -->
    <v-row class="col-12 px-md-10 px-1">
      <div class="col-12 text-sm-end">
        <h1 class="col-md-10 col-12 mx-auto">and save you valuable time</h1>
      </div>
      <v-row class="mb-5 col-md-10 col-12 mx-auto">
        <v-col class="col-sm-10 col-md-6 col-12 mx-auto">
          <p>
            No need to spend time making sense of someone else's data. We collect information about each dataset to
            take out any guesswork on your part. Our
            publishing process also includes a human review to make sure it meets our
            data standards.
          </p>
        </v-col>
        <v-col class="col-sm-10 col-md-6 col-12 mx-auto">
          <v-sheet rounded color="white" elevation="20">
            <v-simple-table dense class="col-12 mb-10">
              <template v-slot:default>
                <thead>
                  <tr>
                    <th class="text-left">
                      Key
                    </th>
                    <th class="text-left">
                      Type
                    </th>
                    <th class="text-left">
                      Units
                    </th>
                    <th class="text-left">
                      Description
                    </th>
                  </tr>
                </thead>
                <tbody>
                  <tr>
                    <td>reference</td>
                    <td>input</td>
                    <td></td>
                    <td>source publication of the band gap value</td>
                  </tr>
                  <tr>
                    <td>structure</td>
                    <td>input</td>
                    <td></td>
                    <td>the structure of this compound</td>
                  </tr>
                  <tr>
                    <td>bandgap value (eV)</td>
                    <td>target</td>
                    <td>eV</td>
                    <td>tvalue of the band gap</td>
                  </tr>
                </tbody>
              </template>
            </v-simple-table>
          </v-sheet>
        </v-col>
      </v-row>
    </v-row>
    <!-- end of row -->

    <v-divider></v-divider>

    <!-- be a part of foundry section -->

    <v-row class="indigo lighten-4 pt-3 pb-10">
      <v-sheet rounded color="indigo lighten-2" elevation="5" class="col-md-8 col-11 mx-auto mt-5">
        <h1 class="text-center my-3 text-h2 white--text font-weight-regular">Build Foundry With Us</h1>
        <p class="col-md-11 col-12 mx-auto white--text font-weight-medium">
          At Foundry, we believe accessibility and collaboration are the keys to
          problem solving. That's why we've made it super easy for you to share
          and use data. If you have a dataset you'd like to contribute, our
          <a class="red--text text--lighten-4"
            href="https://github.com/MLMI2-CSSI/foundry/tree/main/examples/publishing-guides" target="blank">
            publishing guide</a>
          can set you up to do that.
        </p>
        <p class="col-md-11 col-12 mx-auto white--text font-weight-medium">
          Check out our
          <a class="red--text text--lighten-4" href="https://ai-materials-and-chemistry.gitbook.io/foundry/v/docs/"
            target="blank">
            documentation</a>
          to see how easy it is to use Foundry, and follow our
          <a class="red--text text--lighten-4" href="https://github.com/MLMI2-CSSI/foundry/tree/main/examples"
            target="blank">

            examples</a>
          to do it all yourself.
        </p>
      </v-sheet>
    </v-row>

  </div>
</template>

<script>


import { component as VueCodeHighlight } from 'vue-code-highlight';
import "vue-code-highlight/themes/prism-tomorrow.css";
import "vue-code-highlight/themes/window.css";
import 'prism-es6/components/prism-markup-templating';
import 'prism-es6/components/prism-python';

export default {
  name: 'Home',
  components: {
    VueCodeHighlight
  },
  metaInfo: {
    meta: [
      // Twitter Card
      { name: 'twitter:card', content: 'summary' },
      { name: 'twitter:site', content:'@BenBlaiszik'},
      { name: 'twitter:title', content: 'Foundry' },
      { name: 'twitter:description', content: 'ML-ready datasets for materials science and chemistry' },
      // image must be an absolute path
      { name: 'twitter:image', content: 'https://foundry-ml.org/img/logo-full.ec32661a.png' },

      // Facebook OpenGraph
      { property: 'og:type', content: 'article' },
      { property: 'og:title', content: 'Foundry' },
      { property: 'og:site_name', content: 'Vue Example' },
      { property: 'og:image', content: 'https://foundry-ml.org/img/logo-full.ec32661a.png' },
      { property: 'og:description', content: 'ML-ready datasets for materials science and chemistry' }
    ]
  }
}
</script>
