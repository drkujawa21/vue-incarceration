<template>
  <main v-if="!loading">
    <DataTitle :text="title" :date="currentDate" :totalDeaths="totalDeaths"/>

    <DataBoxes :numDeaths="numDeaths" :text="boxTitle"/>

    <PrisonSelect @get-parish="getParishData":prisons="deathRecord" />

    <button 
      @click="clearPrisonData"
      v-if="this.boxTitle"
      class="bg-green-700 text-white rounded p-3 mt-10 focus:outline-none hover:bg-green-600">
      Clear Parish
    </button>
  </main>

  <main class='flex flex-col align-center justify-center text-center' v-else>
    <div class="text-gray-500 text-3xl mt-10 mb-6">
      Fetching Data
    </div>
    <img :src="loadingImage" class="w-24 m-auto" alt="" />
  </main>
</template>

<script>
import DataTitle from '@/components/DataTitle'
import DataBoxes from '@/components/DataBoxes'
import PrisonSelect from '@/components/PrisonSelect'

export default {
  name: 'HomeView',
  components: {
    DataTitle,
    DataBoxes,
    PrisonSelect
  },
  data() {
    return {
      loading: true,
      title: 'Deaths in US parishes',
      boxTitle: "",
      numDeaths: '',
      totalDeaths: '',
      //mostRecent: [],
      currentDate : new Date().toLocaleDateString(),
      deathRecord: [],
      loadingImage: require('../assets/hourglass.gif')
    }
  },
  methods: {
    async fetchAllPrisonData() {
      const res = await fetch('https://incarcerationtransparency.org/api/v1/records/deaths_db/')
      const data = await res.json()
      return data
    },
    //async fetchAllDeathsInXPrison()
    getParishData(parish){
      this.numDeaths = this.deathRecord[parish]
      this.boxTitle = parish
      console.log(this.boxTitle)
    },
    async clearPrisonData(){
      this.loading = true
      const data = await this.fetchAllPrisonData()
      this.numDeaths = 0
      this.boxTitle = "Total"
      this.loading = false
    }
  },
  async created(){
    const data = await this.fetchAllPrisonData()

    const prisonRecords = {}
    data.records.forEach(record => {
      prisonRecords.hasOwnProperty(record.Parish) ? prisonRecords[record.Parish]+=1 : 
        prisonRecords[record.Parish] = 1
    })
    this.deathRecord = prisonRecords

    this.numDeaths= data.records.length //1667
    this.totalDeaths = data.records.length
    
    //this.mostRecent = this.deathRecord[this.numDeaths-1]
    this.loading = false
    console.log(this.deathRecord)
  },
}
</script>
