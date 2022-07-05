<template>
    <div>
        
        <form action="" class="expenses-form">
            <Datepicker class="datepicker" format="dd.MM.yyyy" v-model="card.date"></Datepicker>
            <!-- <input 
            type="text" 
            class="inpt date-inpt" 
            placeholder="enter date..."
            v-model="card.date"
            > -->
            <input 
            type="text" 
            class="inpt amount-inpt" 
            placeholder="enter amount..."
            v-model="card.amount"
            >
            <input 
            type="text" 
            class="inpt currency-inpt" 
            placeholder="enter currency..."
            v-model="card.currency"
            >
            <input 
            type="text" 
            class="inpt product-inpt" 
            placeholder="enter product..."
            v-model="card.product"
            >
            <button
            @click.prevent="createCard" 
            class="inpt-btn"
            >&#10003;</button>
        </form>

        <form class="clear-form">
            <label for="">Enter date and clear all cards with it: </label>
            <Datepicker class="clear-inpt" format="dd.MM.yyyy" v-model="dateForClear"></Datepicker>
            <button @click.prevent="clearCardsWithDate" class="clear-btn">clear</button>
        </form>
    </div>
</template>

<script>
import Datepicker from '@vuepic/vue-datepicker';
import '@vuepic/vue-datepicker/dist/main.css';

export default {     
components: {
    Datepicker
}, 

data(){
    return{
        card: {
            date: null,
            amount: '',
            currency: '',
            product: ''
        },
        dateForClear: null
    }
},
methods: {
    createCard(){
        this.card.id = Date.now()
        this.card.date = JSON.stringify(this.card.date).slice(1, 11)
        this.$emit('create', this.card)
        this.card = {
            date: '',
            amount: '',
            currency: '',
            product: ''
        }
    },
    clearCardsWithDate(){
      this.dateForClear =  JSON.stringify(this.dateForClear).slice(1, 11) 
      this.$emit('clear', this.dateForClear) 
    }
}
}
</script>

<style scoped>
.expenses-form{
    border: 1px solid #c4c4c4;
    border-radius: 5px;
    -webkit-box-shadow: 4px 4px 5px 0px rgba(0,0,0,0.45); 
    box-shadow: 4px 4px 5px 0px rgba(0,0,0,0.45);
    background-color: #c4c4c4;
    padding: 20px;
    display: flex;
    flex-direction: column;
    align-items: center;
}
.datepicker{
    margin-bottom: 15px;
    border-radius: 5px;
    background-color: #f1f1f1;
    width: 100%;
}
.inpt{
    border: none;
    margin-bottom: 15px;
    outline: none;
    border-radius: 5px;
    background-color: #f1f1f1;
    padding: 8px 15px;
    width: 100%;
}
.inpt-btn{
    padding: 6px 20px;
    width: 20%;
    border: none;
    border-radius: 10px;
    font-weight: bold;
    background-color: #3CB371;
    cursor: pointer;
}
.clear-form{
    margin-top: 15px;
    position: relative;
}
.clear-inpt{
    display: inline-block;
   border: none;
    margin-bottom: 15px;
    outline: none;
    border-radius: 5px 0 0 5px;
    background-color: #f1f1f1;
    width: 55%; 
}
.clear-btn{
    position: absolute;
    padding: 11px 20px;
    border: none;
    border-radius: 0 5px 5px 0;
    background-color: #B22222;
    color: #f1f1f1;
    cursor: pointer;
}
</style>