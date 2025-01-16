<template>
    <select @change="onChange()" v-model="selected" 
    class="form-select mt-10 block w-full border p-3 rounded">
        <option value="0">Select Prison</option>
        <option v-for="(prison,value) in prisons" :value="value">
            {{ value }}
        </option>
    </select>
</template>

<script>
    export default {
        name: 'PrisonSelect',
        props: ['prisons'],
        computed: {
            // uniquePrisons: function(){
                
            // },
            // findValue(dict, key){
            //     if(key in dict){
            //         return dict[key];
            //     } else {
            //         return undefined; //return undefined if the key is not found
            //     }
            // }
        },
        data() {
            return {
                selected: 0,
            }
        },
        methods:{
            onChange(){
                //const parish = this.prisons.find((item) => item === this.selected)
                //const parish = findValue(this.prisons, this.selected)
                //const parish = this.prisons[this.selected]
                // if(this.selected in this.prisons){
                //     const parish = this.prisons[this.selected]
                // }
                // else{
                //     const parish = "bruh"
                // }

                this.$emit('get-parish', this.selected)
            },
            
        }
    }
</script>