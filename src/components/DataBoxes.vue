<template>
    <div class="">
        <div class="shadow-md bg-blue-100 p-10 text-center rounded">
            <h3 class="text-3xl text-blue-900 font-bold mb-4">{{ this.boxTitle }}</h3>
            <div class="text-2xl mb-4">
                <span class="font-bold">Deaths:</span>
                {{ numberWithCommas(this.numDeaths) }}  
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "DataBoxes",
        props: ['numDeaths','boxTitle'],
        methods: {
            numberWithCommas(x) {
                if(x => !undefined){
                    return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',')
                }
            }
        }
    }
</script>