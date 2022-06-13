<template>
    <div id="filterForm" class="d-flex flex-row align-center">
        <div style="width: 316px;" class="mr-9">
            <label for="filter">Fitrar por:</label>  
            <v-autocomplete
                id="filter"
                v-model="selected"
                :items="options"
                placeholder="Escolha uma opção"
                item-value="value"
                item-text="text"
                style="margin: 0; padding: 0;"
            ></v-autocomplete>            
        </div>
       
        <div v-if="selected" style="width: 316px;" class="mr-9">
            <label for="filterPerItem">Itens</label>
            <v-autocomplete
                id="filterPerItem"
                v-model="selectedName"
                placeholder="Escolha uma opção"
                :items="optionsName"
                style="margin: 0; padding: 0;"
            ></v-autocomplete>
        </div>
        <v-spacer />
        <v-btn
            @click="getCountry()"
            width="156px"
            elevation="2"
            color="#6D2080"
            style="color: #fff; font-weight: 400; border-radius: 10px;"
        >Pesquisar</v-btn>

    </div>

</template>

<script>

export default {
    name: 'FilterGroup',
    data () {
        return {
            selected: "name",
            selectedName: null,
            cards: [],

            options: [
                { value: "region", text: "Região" },
                { value: "capital", text: "Capital" },
                { value: "lang", text: "Lingua" },
                { value: "name", text: "País" },
            ],
      }

    },

    emits:['getCountry'],

    async created(){
        await this.getCountryAll()
    },
    methods:{
        async getCountryAll(){
            try {
                const countries = await this.$axios.$get('/all')
                this.cards = countries
            } catch (error) {
                console.error(error)
            }
        },
        searchCountriesAndLanguages(item){
            if(this.selected == 'lang'){
                if(item.languages === undefined) return
                const languesArray = Object.keys(item.languages)
                return item.languages[languesArray[0]]
            }
            if(this.selected =='name'){
                return item.name.common
            }
            return item[this.selected]
        },
        getCountry(){
            if(!this.selectedName) return
            this.$emit('getCountry', this.selected, this.selectedName)
        }
    },

    computed: {
        optionsName() {
            let optionsNameSelected = []
            this.cards.map(item => {
                optionsNameSelected.push(this.searchCountriesAndLanguages(item))
            })
            return optionsNameSelected
        }
    }
    
}

</script>

<style>

    #filter,
    #filterPerItem {
        font-size: 18px;
        padding-left: 25px;
        color: #8d8d8d;
    }
    @media screen and (min-width: 320px) and (max-width: 600px) {
        #filterForm {
            display: flex;
            flex-direction: column !important;
            align-items: center !important;
        }
    }
</style>

