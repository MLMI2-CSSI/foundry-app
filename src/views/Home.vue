<template>
  <div class="home col-12 mb-5">
    <!-- heading content -->
    <v-sheet class="text-center py-10 col-12 py-12" color="indigo lighten-2" elevation="12">
      <h1 class="text-h2 col-sm-10 col-12 mx-auto white--text pt-12">
        An open source machine learning platform for scientists
      </h1>
      <v-sheet rounded="xl" elevation="20" class="col-md-6 col-11 mx-auto mt-5 py-1">
        <p class="text-subtitle-1 col-12 my-0 mx-auto indigo--text text--lighten-2 font-weight-medium">
          Accessing ML-ready datasets just became the easiest part of your workflow
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
        <div class="col-sm-10 col-md-6 col-12 mx-auto">
          <vue-code-highlight language="python">
            <pre class="language-python">

  dataset = f.get_dataset("foundry_stan_segmentation_v1.1")
  dataset.get_as_dict()
              
                    </pre>
          </vue-code-highlight>
          <v-sheet rounded color="white" elevation="20">
            <img alt="dendrite segmentation data snippet" src="../assets/dendrite-seg-img.png" class="col-12 pb-3" />
          </v-sheet>
        </div>
        <div class="col-sm-10 col-md-6 col-12 mx-auto">
          <p>
            Foundry-ML hosts structured, ML-ready data of any size that can be accessed programatically with our Python SDK. Once a dataset is uploaded to Foundry-ML, you can load it with just 2
            lines of code. The data is loaded into a DataFrame and ready for analysis!
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
            take out any guesswork on your part.
            Our schema requires key information for every single dataset we host, making it easy to interpret each one.
            Our
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



    <v-row class="indigo lighten-4 pt-3 px-md-10 px-1">
      <h1 class="col-md-10 col-12 mx-auto">Created for sharing large datasets</h1>

      <v-row class="mb-5 col-md-10 col-12 mx-auto">
        <div class="col-sm-10 col-md-6 col-12 mx-auto">
          <p>
            Our infrastructure was built with large datasets in mind. Share data that common infrastructures (email,
            DropBox,
            GitHub) can't. We use <a class="indigo--text text--lighten-1 font-weight-medium" href="https://globus.org"
              target="blank">Globus</a> to easily transfer data to anywhere you want to use it - from a laptop to a
            supercomputer.</p>

          <p>Foundry-ML is part of the <a class="indigo--text text--lighten-1 font-weight-medium"
              href="https://materialsdatafacility.org" target="blank">Materials Data Facility</a>. MDF collects
            high-quality scientific datasets from the community
            and
            makes them easy to find and use.


            Foundry-ML datasets are a
            subset of MDF datasets that are
            structured and can be accessed programatically. For datasets that have less structure, or don't need to
            be accessed programatically, consider using <a class="indigo--text text--lighten-1 font-weight-medium"
              href="https://materialsdatafacility.org" target="blank">MDF</a> directly instead of Foundry-ML.</p>

        </div>
        <div class="col-sm-10 col-md-6 col-12 mx-auto text-center">
          <v-sheet rounded="xl" color="white" class=" col-11 mx-auto py-5">
            <a href="https://globus.org/" target="blank"><img alt="logo" src="../assets/logo_globus.png"
                class="px-6 my-5" /></a>
            <a href="https://materialsdatafacility.org/" target="blank"><img alt="logo" src="../assets/logo_MDF.png"
                class="px-6  my-5" /></a>

          </v-sheet>

        </div>
      </v-row>

    </v-row>



    <!-- be a part of foundry section -->

    <v-row class="mt-8 pt-3 pb-10">
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
  }
}
</script>
