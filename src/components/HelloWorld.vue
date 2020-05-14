<template>
  <div class="rwanda">
    <p>Where are you staying at?🤷‍♂️</p>
    
    <!-- Provinces -->
    <label for="prov">Provinces:</label>
    <select v-model="province" id="prov" class="select">
      <option selected disabled>Select province:</option>
      <option v-for="province in provinces" v-bind:key="province" :value="province">{{province}}</option>
    </select>
    
    <!-- Dedicated districts -->
    <label for="dist">Districts:</label>
    <select v-model="district" id="dist" class="select" @mouseover="loadDistricts">
      <option selected disabled>Select districts:</option>
      <option v-for="district in districts" v-bind:key="district" :value="district">{{district}}</option>
    </select>

    <!-- Dedicated sectors -->
    <label for="sect">Sectors:</label>
    <select v-model="sector" id="sect" class="select" @mouseover="loadSectors">
      <option selected disabled>Select sectors:</option>
      <option v-for="sector in sectors" v-bind:key="sector" :value="sector">{{sector}}</option>
    </select>

    <!-- Dedicated cells -->
    <label for="cell">Cells:</label>
    <select v-model="cell" id="cell" class="select" @mouseover="loadCells">
      <option selected disabled>Select cells:</option>
      <option v-for="cell in cells" v-bind:key="cell" :value="cell">{{cell}}</option>
    </select>
  
    <!-- Dedicated villages -->
    <label for="vill">Villages:</label>
    <select v-model="village" id="vill" class="select" @mouseover="loadVillages" >
      <option selected disabled>Select villages:</option>
      <option v-for="village in villages" v-bind:key="village" :value="village">{{village}}</option>
    </select>
    <h2>You are staying at</h2>
    <div id="place">
      <h3>👨🏾‍🏫Province: <em><span v-html="province"></span></em></h3>
      <h3>📡District: <em><span v-html="district"></span></em></h3>
      <h3>🔐Sector: <em><span v-html="sector"></span></em></h3>
      <h3>📱Cell: <em><span v-html="cell"></span></em></h3>
      <h3>🦹‍♂️Village: <em><span v-html="village"></span></em></h3>
      <h1>🏆</h1>  
    </div>
  </div>
</template>

<script>

const {Provinces, Districts, Sectors, Cells, Villages} = require('rwanda');
export default {
  name: 'HelloWorld',
  data() {
    return {
      village: null,
      villages: [],
      cell: null,
      cells: [],
      sector: null,
      sectors: [],
      district: null,
      districts: [],
      province: null,
      provinces: [],
    }
  },
  mounted() {
    this.provinces = Provinces();
  },
  methods: {
    // loads districts of that specified province
    loadDistricts: function() {
      this.districts = Districts(this.province);
    },
    // loads sectors of that specified district
    loadSectors: function() {
      this.sectors = Sectors(this.province, this.district);
    },
    // loads cells of that specified sector
    loadCells: function() {
      this.cells = Cells(this.province, this.district, this.sector);
    },
    // loads villages of that specified cell
    loadVillages: function() {
      this.villages = Villages(this.province, this.district, this.sector, this.cell);
      // this.$emit("emoji", this.emojicon);
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  /* font */
  @import url('https://fonts.googleapis.com/css2?family=Nunito+Sans&display=swap');

  /* style */
  .rwanda {
    margin-top: 80px;
    font-family: 'Nunito Sans', sans-serif;
  }
  /* #place {
    margin-left: 47%;
    text-align-last: justify;
  } */
  p{
    font-size: 40px;
    margin-bottom: 50px;
  }
  h2 {
    margin-top: 50px;
    margin-bottom: 30px;
    text-decoration: underline;
    
  }
  
  /* span {
    transition: 5s; 
  } */
  label {
    padding-right: 3px;
    padding-left: 6px;
  }
  .select {
    border: 1px solid #ccc;
    width: 120px;
    border-radius: 3px;
    overflow: hidden;
    background: #fafafa;
    position: relative;
    font-size: 16px;
}

  .select:before { 
    content:"\f107"; 
    position: absolute; 
    top:3px; 
    right: 12px; 
    font-size: 18px; }

  .select select {
    padding: 5px 8px;
    width: 130%;
    border: none;
    box-shadow: none;
    background: transparent;
    background-image: none;
    -webkit-appearance: none;
}

  .select select:focus {
    outline: none;
}
</style>
