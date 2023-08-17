<script setup>
import { ref } from 'vue';
import myjson from '../data.json';
let isRed = ref(false);
let xc_id = ref(null);
let xarr = ref([])

let data = ref(myjson)

function redColor(e,x_id){
  if(e.target.checked){
    if(! xarr.value.includes(x_id)){
      xarr.value.push(x_id)
    }
    xc_id.value=x_id
  }else{
    xc_id.value=null
    xarr.value.splice(xarr.value.indexOf(x_id),1)
  }
}
function remove(){
 
  xarr.value.forEach((xa) => {    
    data.value = data.value.filter(el => el.id != xa )
    console.log(data.value)
    
  })  
  
}
</script>

<template>
  <main>
    <div class="container">
      <h1>حساب بانکی</h1>
      <hr/>
      <button @click="remove" type="button" class="btn btn-primary">حذف</button>
      <hr />
      <table class="table">
        <thead>
          <tr>
            <th scope="col"><input type="checkbox"/></th>
            <th scope="col">عنوان حساب</th>
            <th scope="col">شماره حساب</th>
            <th scope="col">شماره شبا</th>
            <th scope="col">وضعیت درگاه بانک</th>
            <th scope="col">وضعیت کارت خوان</th>
          </tr>
        </thead>
        <tbody>
          <tr :class="{red:xarr.includes(x.id) }" v-for="x in data" :key="x.id">
            <td><input type="checkbox" @change="redColor($event,x.id)"/></td>
            <td>{{ x.account_title }}</td>
            <td>{{ x.account_number }}</td>
            <td>{{ x.shaba_number }}</td>
            <td>{{ x.port_status }}</td>
            <td>{{ x.card_reader_status }}</td>        
          </tr>         
        </tbody>
      </table>
    </div>
  </main>
</template>
<style scoped>
.red td{
  background-color: rgb(228, 174, 174);
}
table tbody{
        border-collapse: collapse;
        border-radius: 30px;
        border-style: hidden; /* hide standard table (collapsed) border */
        box-shadow: 0 0 0 1px #666; /* this draws the table border  */ 
    }

    
table thead th{
  background-color: #ccc;
  overflow: hidden;
}    
table thead th:first-of-type{
    border-top-right-radius: 10px; 
}

table thead th:last-of-type{
    border-top-left-radius: 10px; 
}
</style>