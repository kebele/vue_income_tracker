<template>
<!-- 
  video tutorial 
  https://www.youtube.com/watch?v=AjV7k7t78Ik&list=WL&index=5&t=107s
 -->
  <Header :totalIncome="state.totalIncome"/>
  <!-- header a prop olarak state deki totalIncome ı yolluyoruz, Header dan bunu yakalayalım -->
  <Form @add-income="AddIncome"/>
  <IncomeList :state="state" @remove-item="removeItem" />
</template>

<script>
import { reactive, computed } from 'vue';
import Header from './components/Header';
import Form from './components/Form';
import IncomeList from './components/IncomeList';

export default {
  setup() {
    const state = reactive({
      income: [
      //   {
      //   value : 400
      // }, {
      //   value : 600
      // }
      ],
      totalIncome: computed(() => {
        let temp = 0;

        if (state.income.length > 0) {
          for (let i = 0; i < state.income.length; i++) {
            temp += state.income[i].value;
          }
        }

        return temp;
      }),
      sortedIncome : computed(() => {
        let temp = [];

        temp = state.income.sort(function(a,b){
          return b.date - a.date;
        })
        return temp
      })
    });

function AddIncome(data){
// date gösterimi için bir düzenleme yapalım
let d = data.date.split("-")
let newD = new Date(d[0], d[1], d[2])


  state.income = [...state.income, {
    id : Date.now(),
    desc : data.desc,
    value : parseInt(data.value),
    date :  newD.getTime()
  }]
  console.log(state.income)
}

   function removeItem(id) {
      state.income = state.income.filter(v => v.id != id);
    }
    return {
      Header,
      Form,
      state,
      AddIncome,
      IncomeList,
      removeItem
    };
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background: steelblue;
}
</style>
