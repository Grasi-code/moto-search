<template>
<div class="main-container">
    <div class="single-search1">
    <div>
        <input v-model="makerName" type="text" class="form-control" placeholder="Maker of the bike">
        <input v-model="bikeName" type="text" class="form-control" placeholder="Name of the bike">
    </div>
    <button @click="getSpecsRequest1()">Submit</button>
    <p v-for="items in infos" :key="items.articleCompleteInfo">{{items.articleCompleteInfo.makeName}}</p>
    <p v-for="items in infos" :key="items.articleCompleteInfo">{{items.articleCompleteInfo.articleID}}</p>
    <p v-for="items in infos" :key="items.articleCompleteInfo">{{items.articleCompleteInfo.modelName}}</p>
    <p v-for="items in infos" :key="items.articleCompleteInfo">Release Date: {{items.articleCompleteInfo.yearName}}</p>
    <p v-for="items in infos" :key="items.engineAndTransmission">{{items.engineAndTransmission.displacementName}}</p>
    <p v-for="items in infos" :key="items.engineAndTransmission">{{items.engineAndTransmission.powerName}}</p>
    <p v-for="items in infos" :key="items.physicalMeasuresAndCapacities">{{items.physicalMeasuresAndCapacities.weightInclOilGasEtcName}}</p>
    <img src=`${{items?.articleImage?.link}}` alt="test" />
    </div>
    <div class="single-search2">
        <div>
            <input v-model="makerName2" type="text" class="form-control" placeholder="Maker of the bike">
            <input v-model="bikeName2" type="text" class="form-control" placeholder="Name of the bike">
        </div>
        <button @click="getSpecsRequest2()">Submit</button>
        <p v-for="items in infos2" :key="items.articleCompleteInfo">{{items.articleCompleteInfo.makeName}}</p>
        <p v-for="items in infos2" :key="items.articleCompleteInfo">{{items.articleCompleteInfo.modelName}}</p>
        <p v-for="items in infos2" :key="items.articleCompleteInfo">Release Date: {{items.articleCompleteInfo.yearName}}</p>
        <p v-for="items in infos2" :key="items.engineAndTransmission">{{items.engineAndTransmission.displacementName}}</p>
        <p v-for="items in infos2" :key="items.engineAndTransmission">{{items.engineAndTransmission.powerName}}</p>
        <p v-for="items in infos2" :key="items.physicalMeasuresAndCapacities">{{items.physicalMeasuresAndCapacities.weightInclOilGasEtcName}}</p>
        
    </div>
</div>
</template>

<style scoped>

.main-container{
    display: flex;
}

</style>

<script>
export default {
    name: "searchMoto",
    data() {
        return {
            makerName: "Ducati",
            bikeName: "Multistrada V4",
            infos: [],
            makerName2: "",
            bikeName2: "",
            infos2: [],
            img: null

        }
    },
    methods: {
    getSpecsRequest1(){
            fetch('https://motorcycle-specs-database.p.rapidapi.com/make/' + this.makerName + '/model/' + this.bikeName, {method: 'GET', headers: {'X-RapidAPI-Key': '77acf77cc3mshfdbd8eb6e428601p1e30f0jsn2a40ffe7ebec','X-RapidAPI-Host': 'motorcycle-specs-database.p.rapidapi.com'}})
                .then(response => response.json())
                .then((data) => {
                    this.infos = data
                    console.log(this.infos)
                })
                .catch(err => console.error(err));
    },
    getSpecsRequest2(){
            fetch('https://motorcycle-specs-database.p.rapidapi.com/make?populate=*' + this.makerName2 + '/model/' + this.bikeName2, {method: 'GET', headers: {'X-RapidAPI-Key': '77acf77cc3mshfdbd8eb6e428601p1e30f0jsn2a40ffe7ebec','X-RapidAPI-Host': 'motorcycle-specs-database.p.rapidapi.com'}})
                .then(response2 => response2.json())
                .then((data2) => {
                    this.infos2 = data2
                    console.log(this.infos2)
                })
                .catch(err => console.error(err));
    },
    getImgae(){
        fetch('https://motorcycle-specs-database.p.rapidapi.com/make/' + this.makerName + '/model/' + this.bikeName, {method: 'GET', headers: {'X-RapidAPI-Key': '77acf77cc3mshfdbd8eb6e428601p1e30f0jsn2a40ffe7ebec','X-RapidAPI-Host': 'motorcycle-specs-database.p.rapidapi.com'}})
        .then(res => res.blob())
        .then((data) => {
            this.img = data
        })
    }
}
}
</script>