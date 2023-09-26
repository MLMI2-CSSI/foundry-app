<template>
    <div class="datasets">
        <v-container>
            <v-row>
                <h1 class="mx-6 mt-6">Datasets</h1>
            </v-row>
            <v-row class="mx-6 mt-6">
                <v-col>
                    <v-text-field color="blue lighten-1" label="Search" placeholder="Search by title, doi, or author" v-model="input" outlined></v-text-field>
                </v-col>
            </v-row>
            <v-row class="mx-8 mt-n8">
                <v-toolbar>
                    <div  v-for="year in itemYears" class="mx-3">
                        <!-- <input type="checkbox" v-bind:id="year" class="mx-1">
                        <label v-bind:for="year">{{ year }}</label> -->
                        <v-checkbox v-bind:label="year" v-bind:value="year" v-model="yearsInput">

                        </v-checkbox>
                    </div>
                    
                </v-toolbar>
                <div>{{ yearsInput }}</div>
            </v-row>
            <v-row v-if="loaded===true">
                <p class="mx-13 mb-n1 grey--text text--darken-2" >{{filteredItemsLength}} results</p>
            </v-row>
            
            <v-row v-if="loaded===false" style="height: 60vh">
                <v-col cols="6" offset="3" class="d-flex justify-center align-center">
                    <span class="blue--text text--lighten-1 display-4 mdi mdi-dots-circle"></span>
                </v-col>
            </v-row>
            
            <v-row>
                
                <!-- <v-col class="col-md-3 col-12">
                    <v-card class="mx-auto">
                        <v-toolbar color="red lighten-3" dark>
                            <v-toolbar-title>Topics</v-toolbar-title>
                            <v-spacer></v-spacer>
                        </v-toolbar>
                        <v-list>
                            <v-list-group v-for="term in searchTerms" :key="term.title" v-model="term.active"
                                :prepend-icon="term.icon" no-action>
                                <template v-slot:activator>
                                    <v-list-item-content>
                                        <v-list-item-title v-text="term.title"></v-list-item-title>
                                    </v-list-item-content>
                                </template>

                                <v-list-item v-for="child in term.subterms" :key="child.title">
                                    <v-list-item-action>
                                        <v-checkbox color="indigo lighten-3"></v-checkbox>
                                    </v-list-item-action>
                                    <v-list-item-content>
                                        <v-list-item-title v-text="child.title"></v-list-item-title>
                                    </v-list-item-content>
                                </v-list-item>
                            </v-list-group>
                        </v-list>
                    </v-card>
                </v-col> -->
                <v-col>
                    <v-row>
                        <v-card elevation="3"  outlined class="mx-auto col-md-5 col-12 my-6"
                            v-for="item in filteredItems" :key="item.title" :to="item.to" link>
                            <v-card-title class="white-text" style="word-break: keep-all;">{{ item.title }}</v-card-title>
                            <v-card-text>
                                <div class="font-weight-medium">
                                    <span v-for="(author, index) in item.authors" :key="author">
                                        {{ author }}<span v-if="index != item.authors.length - 1">; </span>
                                    </span>
                                </div>
                                <div class="font-weight-medium">
                                    DOI: {{item.dc.identifier.identifier}}
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
                        <v-card elevation="3" class="mx-auto col-md-5 col-12 my-6" v-if="filteredItemsLength === 0 && loaded===true">
                            <v-card-title class="justify-center"  style="word-break: keep-all;">No Results Found</v-card-title>
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
                self.loaded=true


            })
    },
    data: () => ({
        drawer: null,
        items: [],
        input: "",
        yearsInput: [],
        loaded: false,
        testCondition: false,
        facets: { "tags": [] },
        searchTerms: [
            {
                icon: 'mdi-beaker-outline',
                subterms: [{ title: 'this one' }, { title: 'that one' }],
                title: 'Domain',
            },
            {
                icon: 'mdi-run',
                subterms: [
                    { title: 'Classification' },
                    { title: 'Generation' },
                    { title: 'Sushi' },
                ],
                title: 'Task',
            },
            {
                icon: 'mdi-chart-bar',
                subterms: [{ title: 'List Item' }],
                title: 'Data Type',
            },
            {
                icon: 'mdi-file-document',
                subterms: [{ title: 'List Item' }],
                title: 'Data License',
            },
            {
                icon: 'mdi-weight-kilogram',
                subterms: [{ title: 'List Item' }],
                title: 'Size',
            },
            {
                icon: 'mdi-emoticon-neutral',
                subterms: [{ title: 'List Item' }],
                title: 'Mood',
            },
            {
                icon: 'mdi-emoticon-cool',
                subterms: [{ title: 'List Item' }],
                title: 'Vibe',
            },
        ],
    }),
    computed: {
        filteredItems(){
            if(this.input === ""){
                return this.items
            }
            return this.items.filter((item) => {
                return item.title.toLowerCase().includes(this.input.toLowerCase()) || item.dc.identifier.identifier.toLowerCase().includes(this.input.toLowerCase()) || item.authors.map((author)=>author.toLowerCase()).filter((auth) => auth.includes(this.input.toLowerCase())).length != 0
            })
        },
        filteredItemsLength(){
            return this.filteredItems.length
        },
        itemYears(){
            return this.items.map((item) => {
                    return item.dc.dates[0].date.slice(0,4)
                }).filter(function (value, index, arr) {
                    return index == arr.indexOf(value);
                }).sort();
            
        }
    }
}
//authors and DOI
</script>

<style>
    .mdi-dots-circle {
        animation-name: spin;
        animation-duration: 5000ms;
        animation-iteration-count: infinite;
        animation-timing-function: linear; 
}

@keyframes spin {
    from {
        transform:rotate(0deg);
    }
    to {
        transform:rotate(360deg);
    }
}
</style>
