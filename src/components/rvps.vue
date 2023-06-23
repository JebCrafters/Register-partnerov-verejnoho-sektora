<template>
    <div class="container">
        <input type="text" v-model="ico" />
        <button class="searchBtn" v-on:click="getData"> Najst za ICO</button>
        <div class="persons">
            <MyPerson v-for="person in datas" :person="person" :key="person.Id" />
        </div>
    </div>
</template>

<script>
import MyPerson from "./person.vue"
export default {
    name: 'myRvps',
    components: {
        MyPerson
    },
    data() {
        return {
            ico: 44543832,
            datas: null,
            partnerId: null,
            partner: null
        };
    },
    methods: {
        async getData() {
            try {
                const url = 'https://corsproxy.io/?' + encodeURIComponent(`https://rpvs.gov.sk/OpenData/PartneriVerejnehoSektora?$filter=Ico%20eq%20'${this.ico}'&$expand=Adresa`);
                const urlId = 'https://corsproxy.io/?' + encodeURIComponent(`https://rpvs.gov.sk/OpenData/PartneriVerejnehoSektora?$filter=Ico%20eq%20'${this.ico}'&$expand=Partner`);
                const response = await fetch(url, {
                    headers: {
                        'Accept': 'application/json',
                        'Host': 'rpvs.gov.sk',
                    }
                });
                const responseId = await fetch(urlId, {
                    headers: {
                        'Accept': 'application/json',
                        'Host': 'rpvs.gov.sk',
                    }
                });

                if (!response.ok) {
                    throw new Error('Error')
                }
                if (!responseId.ok) {
                    throw new Error('Error')
                }
                const dataId = await responseId.json()
                const data = await response.json()
                // this.partnerId = dataId.value
                this.datas = data.value
                this.partner = dataId.value
                let dataVal = data.value
                let datIdaVal = dataId.value
                for (let i = 0; i < dataVal.length; i++) {
                    for (let j = 0; j < datIdaVal.length; j++) {
                        if (dataVal[i].Id == datIdaVal[j].Id) {
                            dataVal[i].Partner = datIdaVal[j].Partner
                        }
                    }
                }
            } catch (error) {
                console.error(error)
            }
        },
    },
    // watch: {
    //     partnerId(newValue) {
    //         this.getDataPerthons(newValue)
    //     }
    // }
}
</script>

<style scoped>
.container {
    margin-top: 5vh;
    padding-top: 5vh;
    width: 80%;
    height: 80vh;
    background: rgba(110, 110, 110, 0.664);
    display: flex;
    flex-direction: column;
    align-items: center;
}

.searchBtn {
    text-align: center;
    align-items: center;
    width: 5vw;
    height: 3vh;
    background: rgb(26, 214, 136);
    font-size: 2vh;
    width:auto;
    height: auto;
    cursor: pointer;
    margin-top: 2vh;
}

.persons {
    display: grid;
    margin-top: 10vh;
    grid-template-columns: repeat(2, 1fr);
    grid-column-gap: 5vw;
    grid-row-gap: 10vh;
    justify-items: center;
    align-items: center;
    justify-content: center;
    align-content: center;
}
input {
    font-size: 2vh;
    width:auto;
    height: auto;
}
</style>