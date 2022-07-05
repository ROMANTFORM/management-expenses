<template>
  <main>
    <button @click="fetchCurrency">GET CURRENCY</button>
    <p><span>the total amount you spent: </span>{{total}} PLN</p>
    <ExpensesForm 
    @create="createCard"
    @clear="clearCards"
    />
    <div class="expenses-list">
      <ExpensesCard :cards='cards' @delete="deleteCard"/>
    </div>
  </main>
</template>

<script>
import ExpensesForm from './components/ExpensesForm.vue';
import ExpensesCard from './components/ExpensesCard.vue';
// import axios from 'axios';

export default {
  name: 'App',
  components: {
    ExpensesForm,
    ExpensesCard,
  },

  data(){
    return {
      cards: [
        {
          id: 1,
          date: '20.06.2022',
          amount: '12',
          currency: 'USD',
          product: 'banan'
        },
      ],
      total: null
    }
  },

  methods: {
    createCard(card){
      this.cards.push(card)
    },
    deleteCard(card){
      this.cards = this.cards.filter(el => el.id !== card.id)
    },
    clearCards(value){
     this.cards = this.cards.filter(el => el.date !== value) 
    },
    fetchCurrency(){
     const total = this.cards.reduce((sum, el) => sum + +el.amount, 0);
     this.total = total;

      var myHeaders = new Headers();
      myHeaders.append("apikey", "MP1aShzzY6ElWq6oWO7IqhkiwIDJMgLK");

      var requestOptions = {
        method: 'GET',
        redirect: 'follow',
        headers: myHeaders
      };

      fetch(`https://api.apilayer.com/fixer/convert?to=PLN&from=USD&amount=${total}`, requestOptions)
        .then(response => response.text())
        .then(data => {
         const objResult = JSON.parse(data);
         this.total = objResult.result
        })
        .catch(error => console.log('error', error));

      // try{
      //   const res = await axios.get('https://data.fixer.io/api/latest');
      //   console.log("response---->", res)
      // } catch(e){
      //   console.log('ERROR')
      // }
    }
  }, 
}
</script>

<style>
* {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
main {
  max-width: 750px;
  margin: 0 auto;
  padding: 20px 0;
}
.expenses-list{
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 15px;
  margin-top: 15px;
}
</style>
