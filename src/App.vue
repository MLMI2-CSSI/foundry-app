<template>
  <v-app id="inspire">
    <!-- mobile nav -->
    <v-navigation-drawer disable-resize-watcher v-model="drawer" app null class="d-xl-none d-lg-none d-md-none">
      <img alt="Foundry logo icon" src="./assets/logo-full.png" style="width: 200px" />
      <v-divider></v-divider>
      <v-list dense nav>
        <v-list-item v-for="item in items" :key="item.title">
          <a :href="item.to" class="text-decoration-none grey--text text--darken-2">
            <v-list-item-icon class="d-inline">
              <v-icon class="d-inline" color="indigo lighten-1 ">{{ item.icon }}</v-icon>
            </v-list-item-icon>
            <v-list-item-content class="d-inline">
              <v-list-item-title class="d-inline">{{ item.title }}</v-list-item-title>
            </v-list-item-content>
          </a>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar app color="white">
      <v-app-bar-nav-icon class="d-md-none d-lg-none d-xl-none" @click="drawer = !drawer"></v-app-bar-nav-icon>
      <!-- desktop nav bar -->
      <a href="/" class="d-none d-md-flex">
        <v-toolbar-title>
          <img alt="Foundry logo icon" src="./assets/logo-full.png" style="width: 200px" />
        </v-toolbar-title>
      </a>

      <v-spacer class="d-none d-md-flex"></v-spacer>

      <v-toolbar-items class="d-none d-md-flex" v-for="item in items" :key="item.title">
        <a :href="item.to" class="text-decoration-none indigo--text text--darken-1" :target="item.target">
          <v-toolbar-title class="mx-4 mt-4 text-body-1">{{ item.title }}</v-toolbar-title>
        </a>
      </v-toolbar-items>
    </v-app-bar>


    <v-main>
      <router-view></router-view>
    </v-main>
    <v-footer padless color="white" class="col-12 mx-0 px-0 mt-10">
      <v-sheet color="indigo lighten-2" elevation="12" class="mx-auto text-center mt-10 pb-3 pt-10 col-12">
        <v-sheet rounded="xl" color="white" class="col-md-9 col-11 mx-auto">
          <a target="blank" href="https://www.uchicago.edu/"><img alt="logo" src="./assets/logo_UC.png"
              class="px-8" /></a>
          <a target="blank" href="https://www.wisc.edu/"><img alt="logo" src="./assets/logo_UW.png" class="px-8" /></a>
          <a target="blank" href="https://www.nsf.gov/"><img alt="logo" src="./assets/logo_NSF.png" class="px-8" /></a>
          <a target="blank" href="https://www.anl.gov/"><img alt="logo" src="./assets/logo_ANL.png" class="px-8" /></a>
        </v-sheet>
        <p class="pt-5 col-md-8 col-11 mx-auto font-weight-light white--text">This work was supported by the <a
            class="red--text text--lighten-4" target="blank" href="https://www.nsf.gov/">National
            Science
            Foundation</a> under NSF Award Number: 1931306 "Collaborative Research: Framework: Machine Learning
          Materials
          Innovation Infrastructure".</p>
        <p class=" col-md-8 col-11 mx-auto font-weight-light white--text">This work was performed under financial
          assistance award 70NANB14H012 from U.S. Department of Commerce, National Institute of Standards and
          Technology
          as part of the <a class="red--text text--lighten-4" href="https://chimad.northwestern.edu/"
            target="blank">Center for Hierarchical Material
            Design (CHiMaD)</a>.</p>


        <div class="mx-auto">
          <a href="https://materialsdatafacility.org/" target="blank"><img alt="logo" src="./assets/logo_MDF.png"
              class="px-6" /></a>
          <a href="https://globus.org/" target="blank"><img alt="logo" src="./assets/logo_globus.png"
              class="px-6" /></a>
        </div>
        <v-card-text class="white--text pt-3  mx-auto text-body-1">
          <v-icon color="white" class="pb-3">mdi-arm-flex</v-icon> Powered by <a
            class="red--text text--lighten-4 font-weight-bold" href="https://materialsdatafacility.org/"
            target="blank">MDF</a> and <a class="red--text text--lighten-4 font-weight-bold"
            href="https://www.globus.org/" target="blank">Globus</a>.
        </v-card-text>

        <v-divider class="mx-auto" width="90%" color="white"></v-divider>

        <v-card-text class="white--text">
          {{ new Date().getFullYear() }} — <strong>Foundry</strong>
        </v-card-text>
      </v-sheet>
    </v-footer>

  </v-app>
</template>

<script>

export default {
  data: () => ({
    drawer: false,
    items: [
      { title: 'Home', icon: 'mdi-home', to: '/', target: '' },
      { title: 'Datasets', icon: 'mdi-magnify', to: '#/datasets', target: '' },
      { title: 'Documentation', icon: 'mdi-file-document-multiple-outline', to: 'https://ai-materials-and-chemistry.gitbook.io/foundry/v/docs/', target: 'blank' },
      { title: 'Examples', icon: 'mdi-rocket-launch', to: `https://github.com/MLMI2-CSSI/foundry/tree/main/examples`, target: 'blank' }
    ]
  }),
}
</script>