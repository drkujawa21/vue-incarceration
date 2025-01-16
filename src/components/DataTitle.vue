<template>
    <div class="text-center">
        <h2 class="text-3xl font-bold">{{ text }}</h2>
        <div class="text-2xl mt-4 mb-10">{{ numberWithCommas(totalDeaths) }} as of {{ date }}</div>
    </div>
</template>

<script>
import moment from 'moment'

    export default {
        name: 'DataTitle',
        props: ['text', 'date', 'totalDeaths'],
        computed: {
            
        },
        methods: {
            numberWithCommas(x) {
                if(x => !undefined){
                    return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',')
                }
            }
        }
    }
</script>