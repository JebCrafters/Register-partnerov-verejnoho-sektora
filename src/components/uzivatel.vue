<template>
    <div class="containerUzivatel">
        <span v-if="uzivatel.Meno">{{ 'Meno: ' + uzivatel.Meno }}</span>
        <span v-if="uzivatel.Priezvisko">{{ 'Meno: ' + uzivatel.Priezvisko }}</span>
        <span v-if="uzivatel.DatumNarodenia">{{ 'Datum Narodenia: ' + uzivatel.DatumNarodenia }}</span>
        <span v-if="uzivatel.TitulPred">{{ 'Titul Pred: ' + uzivatel.TitulPred }}</span>
        <span v-if="uzivatel.TitulZa">{{ 'Titul Za: ' + uzivatel.TitulZa }}</span>
        <span v-if="uzivatel.JeVerejnyCinitel">{{ 'Je Verejny Cinitel: ' + uzivatel.JeVerejnyCinitel }}</span>
        <span v-if="uzivatel.ObchodneMeno">{{ 'Obchodne Meno: ' + uzivatel.ObchodneMeno }}</span>
        <span v-if="uzivatel.Ico">{{ 'Ico: ' + uzivatel.Ico }}</span>
        <span v-if="uzivatel.PlatnostOd">{{ 'Platnost Od: ' + uzivatel.PlatnostOd }}</span>
        <span v-if="uzivatel.PlatnostDo">{{ 'Platnost Do: ' + uzivatel.PlatnostDo }}</span>
    </div>
</template>

<script>
    export default {
        name: 'myUzivatel',
    props: {
        uzivatela: Object,
    },
    data() {
        return {
           uzivatel: this.uzivatela
        };
    },
    }
</script>

<style scoped>
span {
    font-size: 2vh;
    width:auto;
    height: auto;
}
.containerUzivatel {
    display: flex;
    flex-direction: column;
    width: 25vw;
    overflow: auto;
    align-items: center;
    text-align: center;
}
</style>