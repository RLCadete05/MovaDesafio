<template>
    <div>
        <v-card
            class="mb-10"
            style="cursor: pointer;"
            width="316"
            tile
            @click="toCountry()"
        >
            <v-img 
                height="181" 
                :src="card.flags.png"
            ></v-img>
        </v-card>
    </div>
</template>

<script>
export default {
    name: 'FlagsCard',
    props: {
        card: Object
    },
    methods: {
        toCountry(){
            this.$router.push({ path: `/country/${this.card.name.common}` })
        }
    }
}
</script>