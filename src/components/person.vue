<template>
    <div class="containers">
        <div v-show="!showFullInfo" class="baseInfo">
            <h3>Udaje partnera verejného sektora</h3>
            <span v-if="udaje.ObchodneMeno">{{ 'Obchodne Meno: ' + obchodneMeno }}</span>
            <span v-if="udaje.Meno">{{ 'Meno: ' + udaje.Meno }}</span>
            <span v-if="udaje.Priezvisko">{{ 'Priezvisko: ' + udaje.Priezvisko }}</span>
            <span v-if="udaje.DatumNarodenia">{{ 'Datum Narodenia: ' + udaje.DatumNarodenia }}</span>
            <span v-if="udaje.FormaOsoby">{{ 'Forma Osoby: ' + udaje.FormaOsoby }}</span>
            <span>{{ 'ICO : ' + udaje.Ico }}</span>
            <div class="adres">
                <h3>Adress</h3>
                <span v-if="udaje.Adresa.Mesto">{{ 'Mesto: ' + this.udaje.Adresa.Mesto }}</span>
                <span v-if="udaje.Adresa.MenoUlice">{{ 'Meno Ulice: ' + this.udaje.Adresa.MenoUlice }}</span>
                <span v-if="udaje.Adresa.OrientacneCislo">{{ 'Orientacne Cislo: ' + this.udaje.Adresa.OrientacneCislo
                }}</span>
                <span v-if="udaje.Adresa.Psc">{{ 'Psc: ' + this.udaje.Adresa.Psc }}</span>
            </div>
            <button class="searchBtn" v-on:click="getPerson">Získajte úplné informácie</button>
        </div>

        <div v-if="showFullInfo" class="containerFullInfo">
            <div class="backgroundFullInfo">
                <h1>{{ null }}</h1>
            </div>
            <div class="fullinfo">
                <button class="btnBack" v-on:click="backToBaseInfo">BACK</button>
                <span v-if="udaje.ObchodneMeno">{{ 'Obchodne Meno: ' + obchodneMeno }}</span>
                <span v-if="udaje.Meno">{{ 'Meno: ' + udaje.Meno }}</span>
                <span v-if="udaje.Priezvisko">{{ 'Priezvisko: ' + udaje.Priezvisko }}</span>
                <span v-if="udaje.DatumNarodenia">{{ 'Datum Narodenia: ' + udaje.DatumNarodenia }}</span>
                <span v-if="udaje.FormaOsoby">{{ 'Forma Osoby: ' + udaje.FormaOsoby }}</span>
                <span v-if="udaje.TitulPred">{{ 'Titul Pred: ' + udaje.TitulPred }}</span>
                <span v-if="udaje.TitulZa">{{ 'Titul Za: ' + udaje.TitulZa }}</span>
                <span v-if="udaje.PlatnostOd">{{ 'Platnost Od: ' + udaje.PlatnostOd }}</span>
                <span v-if="udaje.PlatnostDo">{{ 'Platnost Do: ' + udaje.PlatnostDo }}</span>
                <span>{{ 'ICO : ' + udaje.Ico }}</span>
                <div class="adres">
                    <h3>Adress</h3>
                    <span v-if="udaje.Adresa.Mesto">{{ 'Mesto: ' + this.udaje.Adresa.Mesto }}</span>
                    <span v-if="udaje.Adresa.MenoUlice">{{ 'Meno Ulice: ' + this.udaje.Adresa.MenoUlice }}</span>
                    <span v-if="udaje.Adresa.OrientacneCislo">{{ 'Orientacne Cislo: ' + this.udaje.Adresa.OrientacneCislo
                    }}</span>
                    <span v-if="udaje.Adresa.Psc">{{ 'Psc: ' + this.udaje.Adresa.Psc }}</span>
                </div>
                <div class="uzivatelaContainer">
                    <h3>Uzivatela</h3>
                    <div class="uzivatela">
                        <Uzivatel v-for="uzivatel in konecniUzivatel" :uzivatela="uzivatel" :key=uzivatel.Id />
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Uzivatel from './uzivatel'
import uzivatel from "./uzivatel.vue"
export default {
    name: 'myPerson',
    props: {
        person: Object,
    },
    components: {
        Uzivatel,
        uzivatel
    },
    data() {
        return {
            obchodneMeno: this.person.ObchodneMeno,
            udaje: this.person,
            adresa: this.person.Adresa,
            partnerId: this.person.Partner.Id,
            showFullInfo: false,
            konecniUzivatel: null
        };
    },
    methods: {
        getPerson() {
            const url = 'https://corsproxy.io/?' + encodeURIComponent(`https://rpvs.gov.sk/OpenData/Partneri(${this.partnerId})?$expand=KonecniUzivateliaVyhod%20`)

            fetch(url, {
                headers: {
                    'Accept': 'application/json',
                    'Host': 'rpvs.gov.sk',
                }
            })
                .then(function (response) {
                    return response.json()
                })
                .then((data) => {
                    console.log(data.KonecniUzivateliaVyhod)
                    this.konecniUzivatel = data.KonecniUzivateliaVyhod
                })
            this.showFullInfo = true
        },
        backToBaseInfo() {
            this.showFullInfo = false
        }
    }
}
</script>

<style  scoped>
span {
    font-size: 2vh;
    width:auto;
    height: auto;
}
.containers, .adres, .baseInfo  {
    margin: 0;
    display: flex;
    flex-direction: column;
    height: 100%;
    width: 100%;
    max-width: 30vw;
    align-items: center;
    text-align: center;
}
h3 {
    padding-top: 1vh;
    font-size: 3vh;
    text-align: center;
}

.searchBtn {
    z-index: 0;
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
.containerFullInfo {
    height: auto !important;
}

.backgroundFullInfo {
    z-index: 5;
    display: flex;
    position: fixed;
    top: 0;
    left: 0%;
    width: 100vw;
    height: 100%;
    background: rgb(109, 109, 109);
}

.fullinfo {
    z-index: 6;
    display: flex;
    flex-direction: column;
    position: absolute;
    top: 10%;
    bottom: 10%;
    left: 20%;
    width: auto;
    height: auto;
    background: rgb(202, 202, 202);
    justify-content: center;
    align-items: center;
    border-radius: 15%;
    border: 1px solid black;
    padding-top: 15%;
    padding-bottom: 15%;
    overflow: hidden;
}

.uzivatelaContainer {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 0 10%;
}

.uzivatela {
    display: grid;
    margin-top: 2vh;
    grid-template-columns: repeat(2, 1fr);
    grid-column-gap: 15vw;
    grid-row-gap: 10vh;
    justify-items: center;
    align-items: center;
    justify-content: center;
    align-content: center;
}
.btnBack {
    position: absolute;
    top: 10vh;
    left: 5vw;
    border-radius: 10%;
    border: 1px solid black;
    background:yellow;
    cursor: pointer;
    font-size: 3vh;
}
</style>