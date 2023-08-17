<script setup>
import { ref } from 'vue';
import myjson from '../data.json';
let isRed = ref(false);
let xc_id = ref(null);
let xarr = ref([])

let data = ref(myjson)

let card_reader_status = ref(null)
let port_status = ref(null)

function redColor(e, x_id) {
  if (e.target.checked) {
    if (!xarr.value.includes(x_id)) {
      xarr.value.push(x_id)
    }
    xc_id.value = x_id
  } else {
    xc_id.value = null
    xarr.value.splice(xarr.value.indexOf(x_id), 1)
  }
}
function remove() {

  xarr.value.forEach((xa) => {
    data.value = data.value.filter(el => el.id != xa)
    console.log(data.value)

  })

}

function search(){
  if(card_reader_status.value == 'not'){
    data.value = myjson
  }
  if(card_reader_status.value == 1){
    data.value = data.value.filter(el => el.card_reader_status == true)
  }
  if(card_reader_status.value == 2){
    data.value = data.value.filter(el => el.card_reader_status == false)
  }
  if(port_status.value == 'not'){
    data.value = myjson
  }
  if(port_status.value == 1){
    data.value = data.value.filter(el => el.port_status == true)
  }
  if(port_status.value == 2){
    data.value = data.value.filter(el => el.port_status == false)
  }
}
function more(){
  console.log('more')
  data.value.push(
    {
        "id":uuidv4(),
        "account_title": "ملت",
        "account_number": "3443655465",
        "shaba_number": "6464645",
        "port_status": true,
        "card_reader_status": false
    }
  )
  console.log(data.value)
}

function uuidv4() {
  return ([1e7]+-1e3+-4e3+-8e3+-1e11).replace(/[018]/g, c =>
    (c ^ crypto.getRandomValues(new Uint8Array(1))[0] & 15 >> c / 4).toString(16)
  );
}
</script>

<template>
  <main>
    <div class="container">
      <h1>حساب بانکی</h1>
      <hr />
      <button @click="remove" type="button" class="btn btn-danger">حذف</button>
      <hr />
      <form class="row g-3">        
        <div class="col-auto">
          <select v-model="card_reader_status" class="form-select" aria-label="Default select example">
            <option value="not" selected>همه کارت خوان ها</option>
            <option value="1">فعال</option>
            <option value="2">غیرفعال</option>
          </select>
        </div>
        <div class="col-auto">
          <select v-model="port_status" class="form-select" aria-label="Default select example">
            <option value="not" selected>همه درگاه ها</option>
            <option value="1">فعال</option>
            <option value="2">غیرفعال</option>
          </select>
        </div>
        <div class="col-auto">
          <button @click="search" type="button" class="btn btn-primary mb-3">جستجو</button>
        </div>
      </form>
      <table class="table">
        <thead>
          <tr>
            <th scope="col"><input type="checkbox" /></th>
            <th scope="col">عنوان حساب</th>
            <th scope="col">شماره حساب</th>
            <th scope="col">شماره شبا</th>
            <th scope="col">وضعیت درگاه بانک</th>
            <th scope="col">وضعیت کارت خوان</th>
          </tr>
        </thead>
        <tbody>
          <tr :class="{ red: xarr.includes(x.id) }" v-for="x in data" :key="x.id">
            <td><input type="checkbox" @change="redColor($event, x.id)" /></td>
            <td>{{ x.account_title }}</td>
            <td>{{ x.account_number }}</td>
            <td>{{ x.shaba_number }}</td>
            <td>{{ x.port_status }}</td>
            <td>{{ x.card_reader_status }}</td>
          </tr>
        </tbody>
      </table>
      <div class="more">
        <button @click="more" type="button" class="btn btn-light">مشاهده بیشتر</button>
      </div>
    </div>
  </main>
</template>
<style scoped>
.more{
  text-align: center;
}
.red td {
  background-color: rgb(228, 174, 174);
}

table tbody {
  border-collapse: collapse;
  border-radius: 30px;
  border-style: hidden;
  /* hide standard table (collapsed) border */
  box-shadow: 0 0 0 1px #666;
  /* this draws the table border  */
}


table thead th {
  background-color: #ccc;
  overflow: hidden;
}

table thead th:first-of-type {
  border-top-right-radius: 10px;
}

table thead th:last-of-type {
  border-top-left-radius: 10px;
}
</style>