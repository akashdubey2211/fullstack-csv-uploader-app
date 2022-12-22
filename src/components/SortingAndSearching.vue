<template>
    <div>
      <h2>Csv Uploader &#128203;</h2>
      <div class="row">
        <div class="col">
          <input
              type="text"
              v-model.trim="search"
              placeholder="Search by Name..."
              @keyup="getAllStarWarsPeople"
            /><br />
        </div>
        <div class="col">
            <Upload />
        </div>
    </div>

      <table>
        <tr>
          <th @click="sortList('SSN')">ID &#8597;</th>
          <th @click="sortList('FirstName')">Name &#8597;</th>
          <th @click="sortList('LastName')">Email &#8597;</th>
          <th @click="sortList('Final')">Name &#8597;</th>
          <th @click="sortList('Grade')">Email &#8597;</th>
        </tr>
        <tr v-for="(data, index) in sortedData" :key="index">
          <td>{{ data.SSN }}</td>
          <td>{{ data.FirstName }}</td>
          <td>{{ data.LastName }}</td>
          <td>{{ data.Final }}</td>
          <td>{{ data.Grade }}</td>
        </tr>
      </table>
      <div style="padding-top: 10px">wwww.nightprogrammer.com</div>
    </div>
  </template>
  
  <script>
import Upload from './Upload.vue';

  export default {
    name: "PrepVue",
    data() {
        return {
            sortedData: [],
            sortedbyASC: true,
            search: ""
        };
    },
    mounted() {
        this.sortedData;
        console.log(this.sortedData);
    },
    methods: {
        getAllStarWarsPeople() {
            fetch("http://localhost:4000")
                .then(response => response.json())
                .then(res => {
                console.log(res);
                if (this.search) {
                    console.log(res);
                    this.sortedData = res.data.filter(sortedData => sortedData.FirstName.toLowerCase().includes(this.search.toLowerCase()));
                }
                else {
                    this.sortedData = res.data;
                }
            });
        },
        sortList(sortBy) {
            if (this.sortedbyASC) {
                this.sortedData.sort((x, y) => (x[sortBy] > y[sortBy] ? -1 : 1));
                this.sortedbyASC = false;
            }
            else {
                this.sortedData.sort((x, y) => (x[sortBy] < y[sortBy] ? -1 : 1));
                this.sortedbyASC = true;
            }
        },
    },
    created() {
        this.getAllStarWarsPeople();
    },
    components: { Upload }
};
  </script>
  
  <style>
  input[type=text] {
    width: 100%;
    padding: 12px 20px;
    margin: 8px 0;
    display: inline-block;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-sizing: border-box;
  }
  
  table {
    font-family: arial, sans-serif;
    border-collapse: collapse;
    width: 100%;
  }
  
  td,
  th {
    border: 1px solid #dddddd;
    text-align: left;
    padding: 8px;
  }
  
  th:hover {
    cursor: pointer;
    background: rgb(229, 255, 211);
  }
  
  tr:nth-child(even) {
    background-color: #f3f3f3;
  }
  </style>