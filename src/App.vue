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

  mounted(){
    // --------------- Task 1 ------------------------------>
function sortString(str){
const arrOfStrings = str.split(' ');
const sortedElArr = arrOfStrings.sort((a, b) => {
    a = +/\d+/.exec(a);
    b = +/\d+/.exec(b)
    return a - b
}); 
console.log(sortedElArr.join(' '))
}
sortString("g5et ski3lls on6 use1 your2 to4 7top");
sortString("");
sortString("practic3 h4rder yo1u 2hould");

// ---------------- Task 2 ------------------------------->
function queueTime(customers, n) {
    var sorted = customers.sort((a,b)=>b-a);
    
    var tills = Array(n).fill(0);
    
    while(sorted.length>0){
      for(var i=0;i<n && i<sorted.length;i++)
      {
        tills[i] += sorted.shift();
      }
      tills = tills.sort((a,b)=>a-b);
    }
    console.log(Math.max(...tills))
    return Math.max(...tills);
  }
// function queueTime(arr, num){
//     if(num === 1){
//        let total = arr.reduce((sum, el) => {
//         return sum + el
//     }, 0);
//     console.log("Если очередь одна, то общее время: ", total);
//     } else {
//         let allTime = [];
//         for(let i = 0; i < arr.length; i += arr.length/num){
//             const chunk = arr.slice(i, i + arr.length/num);
//             let totalArr = chunk.reduce((sum, el) => {
//                 return sum + el
//             });
//             allTime.push(totalArr)
//         }
//         console.log("если очередей больше одной, то самая долгая очередь: ", Math.max.apply(null, allTime))
//     }
// };
queueTime([5, 3, 4, 6, 2, 3], 3);
queueTime([5,3,4], 1)
// Output: 12 (5 + 3 + 4)
queueTime([10, 2, 3, 3], 2)
// 4 customers that require 10, 2, 3 and 3 minutes respectively and 2 checkout
// Output: 10
queueTime([], 1);
// Output: 0

// ------------------------ Task 3 ------------------------------------->
function biggerNumber(num){
const sortedArr = num.toString(10).split('').sort((a, b) => { return b - a});
const sortedNum = sortedArr.join('');

if(num >= +sortedNum){
    console.log(-1); 
} else if(sortedArr.length === 1){
    console.log(-1);   
} else {
    console.log(+sortedNum);
}
}
biggerNumber(23) // 32;
biggerNumber(624) // 642;
biggerNumber(2018) // 8210;
// If there is no greater number, return -1
biggerNumber(9) // = -1;
biggerNumber(111) // = -1;
biggerNumber(531) // = -1;

  }
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
