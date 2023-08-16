<script setup>
import myjson from '../data.json';
</script>

<template>
  <main>
    <div class="container">
      <h1>حساب بانکی</h1>
      <table class="table">
        <thead>
          <tr>
            <th>عنوان حساب</th>
            <th>شماره حساب</th>
            <th>شماره شبا</th>
            <th>وضعیت درگاه بانک</th>
            <th>وضعیت کارت خوان</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="x in myjson">
            <th>{{ x.account_title }}</th>
            <th>{{ x.account_number }}</th>
            <th>{{ x.shaba_number }}</th>
            <th>{{ x.port_status }}</th>
            <th>{{ x.card_reader_status }}</th>        
          </tr>         
        </tbody>
      </table>
    </div>
  </main>
</template>
<style scoped>
table {
        border-collapse: collapse;
        border-radius: 30px;
        border-style: hidden; /* hide standard table (collapsed) border */
        box-shadow: 0 0 0 1px #666; /* this draws the table border  */ 
    }

    td {
        border: 1px solid #ccc;
    }
</style>