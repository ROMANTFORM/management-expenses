<template>
    <div class="expenses-card" v-for="card in cards" :key="card.id">
        <p class="card__text card__date"><span>Date: </span>{{card.date}}</p>
        <hr/>
        <p class="card__text card__amount"><span>Amount of money: </span>{{card.amount}}</p>
        <hr/>
        <p class="card__text card__currency"><span>Currency: </span>{{card.currency.toUpperCase()}}</p>
        <hr/>
        <p class="card__text card__product"><span>Product: </span>{{card.product}}</p>
        <hr/>
        <button class="del-btn" @click="$emit('delete', card)">&#10008;</button>
    </div>
</template>

<script>

export default {
props: ['cards'],

}
</script>

<style scoped>
.expenses-card{
    border: 1px solid #c4c4c4;
    border-radius: 5px;
    -webkit-box-shadow: 4px 4px 5px 0px rgba(0,0,0,0.45); 
    box-shadow: 4px 4px 5px 0px rgba(0,0,0,0.45);
    padding: 20px;
}
.card__text{
    color: #313131;
    font-weight: bold;
    display: grid;
    grid-template-columns: 1fr 1fr;
    margin-top: 10px;
    align-items: end;
}
.card__text span{
    font-weight: 300;
}
.del-btn{
    border: none;
    padding: 5px 20px;
    cursor: pointer;
    border-radius: 25px;
    background-color: #CD5C5C;
    margin-top: 5px;
}
</style>
