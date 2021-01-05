<template>
    <form @submit.prevent="formHandler()">
        <!-- e.preventDefault() yerine @submit.prevent="..." kullandık -->
        <input type="text" name="" id="" placeholder="description" v-model="formData.desc"/>
        <input type="number" name="" id="" placeholder="value..." v-model="formData.value"/>
        <input type="date" name="" id="" placeholder="date..." v-model="formData.date"/>
        <input type="submit" value="SUBMIT" />
    </form>
</template>

<script>
    import { reactive } from 'vue'


    export default {
        // dışarıdan yani Form comp un kullanıldığı yerden gelecek proplar
        props : {
            state : Object
        },
        // setup (){
        setup (props, { emit }){
            const formData = reactive ({
                desc: null,
                value: null,
                date: null,
            })

            function formHandler(){
                // console.log(formData);
                //UI dan gelen verileri emitleyelim, add-income keyi ile, App.vue dan yakalayalım
                emit("add-income", {
                    desc : formData.desc,
                    value : formData.value,
                    date : formData.date
                })

//inputları boşaltalım
                formData.desc = null
                formData.value = null
                formData.date = null
            }
            return {
                formHandler,
                formData,
            }
        }
    }
</script>

<style scoped>
form {
    display: flex;
    justify-content: center;
    margin-top: 30px;
  }
  form input {
    color: #888;
    border: none;
    outline: none;
    font-size: 20px;
  }
  form input::placeholder {
    color: #AAA;
  }
  form input:not([type="submit"]) {
    display: block;
    background: #FFF;
    border: none;
    outline: none;
    padding: 5px 15px;
  }
  form input[type="submit"] {
    display: block;
    background: none;
    border: none;
    outline: none;
    color: #FFF;
    font-weight: 500;
    text-shadow: 0px 1px 3px rgba(0, 0, 0, 0.2);
    padding: 5px 15px;
    background-color: #FFCE00;
    cursor: pointer;
  }
  form input:first-of-type {
    border-radius: 8px 0px 0px 8px;
  }
  form input:last-of-type {
    border-radius: 0px 8px 8px 0px;
  }
</style>