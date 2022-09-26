<template>
    <div class="datasets">
        <v-container>
            <v-row>
                <h1 class="mx-6 mt-6">Datasets</h1>
            </v-row>
            <v-row>
                <div class="search-wrapper">
                    <input type="text" v-model="searchQuery" placeholder="Search title.." />
                    <label>Search title:</label>
                </div>
            </v-row>
            <v-row>
                <v-col>
                    <v-row>

                        <v-card elevation="3" outlined class="mx-auto col-md-5 col-12 my-6" v-for="item in resultQuery"
                            v-bind:key="item.title" v-bind:to="item.to" link>
                            <v-card-title class="white-text" style="word-break: keep-all;">{{ item.title }}
                            </v-card-title>
                            <v-card-text>
                                <div class="font-weight-medium">
                                    <span v-for="(author, index) in item.authors" :key="author">
                                        {{ author }}<span v-if="index != item.authors.length - 1">; </span>
                                    </span>
                                </div>
                                <div class="font-weight-medium">
                                    DOI: {{ item.dc.identifier.identifier }}
                                </div>

                                <div>
                                    <v-chip class="ma-2" color="blue lighten-1" text-color="white">
                                        {{ item.foundry.data_type }}
                                    </v-chip>

                                    <v-chip class="ma-2" color="red lighten-2" text-color="white">
                                        {{ item.foundry.task_type[0] }}
                                    </v-chip>
                                    <v-chip class="ma-2" color="indigo lighten-3" text-color="white">
                                        {{ item.foundry.n_items }} Items
                                    </v-chip>
                                </div>




                            </v-card-text>
                        </v-card>
                    </v-row>

                </v-col>
            </v-row>
        </v-container>
    </div>
</template>


<!-- This is where the dataset data will be loaded and put into the cards -->
<script>
import axios from 'axios';


export default {
    mounted() {
        var self = this;

        // Define the search endpoint and index
        var ep = 'https://search.api.globus.org/v1/index/1a57bbe5-5272-477f-9d31-343b8258b7a5/search'

        // Format the POST query for Globus search
        // Facet
        var query = {
            "q": "(mdf.organizations:Foundry) AND (mdf.resource_type:dataset)",
            "limit": 100,
            "advanced": true,
            "facets": [
                {
                    "name": "tags",
                    "field_name": "dc.subjects.subject",
                    "type": "terms", //"date_histogram",
                    "size": 20
                }
            ]
        }

        // Perform the POST request, and load the information into the Vue object
        axios
            .post(ep, query)
            .then(function (res) {
                console.log("AXIOS POST")
                console.log(res)
                for (let i = 0; i < res.data.gmeta.length; i++) {
                    // TODO, add more data into the view object for display
                    var creators = res.data.gmeta[i].entries[0].content.dc.creators
                    var authors = []
                    var dataset_link = ""

                    for (let j = 0; j < creators.length; j++) {
                        authors.push(creators[j].creatorName)
                    }

                    console.log(res.data.gmeta[i].entries[0].content.dc.identifier)

                    if (res.data.gmeta[i].entries[0].content.dc.identifier.identifier) {
                        dataset_link = "/datasets/" + encodeURIComponent(res.data.gmeta[i].entries[0].content.dc.identifier.identifier)
                    } else {
                        dataset_link = "/datasets/" + res.data.gmeta[i].entries[0].content.mdf.source_id
                    }

                    self.items.push({
                        "title": res.data.gmeta[i].entries[0].content.dc.titles[0].title,
                        "foundry": res.data.gmeta[i].entries[0].content.projects.foundry,
                        "dc": res.data.gmeta[i].entries[0].content.dc,
                        "authors": authors,
                        "to": dataset_link
                    })
                }

                // Loop through the facet results from Globus Search, and put them 
                // into the facets object
                for (let j = 0; j < res.data.facet_results[0].buckets.length; j++) {
                    self.facets.tags.push({
                        "title": res.data.facet_results[0].buckets[j].value,
                        "count": res.data.facet_results[0].buckets[j].count
                    })
                }

                // Push facet results into the searchTerms for display purposes
                self.searchTerms.push({
                    "icon": 'mdi-beaker-outline',
                    "subterms": self.facets.tags,
                    "title": 'Tag',
                })


            })
    },
    data: () => ({
        drawer: null,
        searchQuery: null,
        items: [],
        facets: { "tags": [] },
        search: '',
        computed: {
            resultQuery() {
                if (this.searchQuery) {
                    return this.items.filter(item => {
                        return this.searchQuery
                            .toLowerCase()
                            .split(" ")
                            .every(v => item.title.toLowerCase().includes(v));
                    });
                } else {
                    return this.items;
                }
            }

        }
    }),
}
</script>
