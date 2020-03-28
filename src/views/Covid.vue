<template>
   <b-container class="mt-5">
     <b-card-group deck>
       <b-card v-for="country in countries" :key="country.country" :title="country.country" :img-src="country.countryInfo.flag" img-alt="Image" img-top>
         <b-card-text>
            <b-row><b-col align="right">Total Cases:</b-col><b-col align="left">{{ country.cases }}</b-col></b-row>
            <b-row><b-col align="right">Total Deaths:</b-col><b-col align="left">{{ country.deaths }}</b-col></b-row>
            <b-row><b-col align="right">Today Cases:</b-col><b-col align="left">{{ country.todayCases }}</b-col></b-row>
            <b-row><b-col align="right">Today Deaths:</b-col><b-col align="left">{{ country.todayDeaths }}</b-col></b-row>
            <b-row><b-col align="right">Active Cases:</b-col><b-col align="left">{{ country.active }}</b-col></b-row>
            <b-row><b-col align="right">Recovered:</b-col><b-col align="left">{{ country.recovered }}</b-col></b-row>
            <b-row><b-col align="right">Critical:</b-col><b-col align="left">{{ country.critical }}</b-col></b-row>
         </b-card-text>
         <template v-slot:footer>
           <small class="text-muted">Last updated 3 mins ago</small>
         </template>
       </b-card>
     </b-card-group>
   </b-container> 
</template>

<script>
import axios from 'axios'

export default {
    name: 'Covid',
    data: function() {
        return {
            countries: []
        }
    },
    computed: {
        loaded: function() {
            let list = []
            for (let country of this.countries) {
                list.push(country.country)
            }
            return list
        }
    },
    created() {
        for (let c of ['USA', 'UK', 'Italy']) {
            this.loadCountry(c);
        }
    },
    methods: {
        loadCountry(code) {
            for (let country of this.loaded) {
                if (code == country) {
                    return false
                }
            }

            axios.get('https://corona.lmao.ninja/countries/' + code)
                .then( resp => {
                    let country = resp.data
                    if (this.countries.length < 3) {
                        this.countries.push(country)
                    } else {
                        this.countries.splice(0, 0, country)
                        this.countries.pop()
                    }
                })
                .catch(error => {
                    alert(error)
                });
        }
    }
}

</script>
