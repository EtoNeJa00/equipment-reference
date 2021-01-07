<template>
  <div class="value">
    <div class="value-over"> Вендоры </div>
    <div v-for="vendor in vendorList" :key="vendor">
    <div class="vendor-block">
      <label> {{vendor}} </label><br/>
        <span>Количество активных элементов: {{getCountElem(response, vendor,"ACTIVE")}}</span>
        <span>Количество отключенных элементов: {{getCountElem(response, vendor,"DISABLE")}}</span>
      <hr>
    </div>
    </div>
    </div>
  <calculator @calculated='Calculated'/>
</template>

<script>
import Calculator from './Calculator.vue'
export default {

    components: {
    Calculator,
  },

  data () {
    return {
      response:[],
    }
  },

  computed: {
    vendorList() {
      let unique = [...new Set(this.response.map(item => item.Vendor))];
      return unique;
    }
  },

  methods: {
    getCountElem(value, vendor, status) {
    if (!value) return '';
    let counter = 0;
    for(let i=0;i<value.length;i++){
      if(value[i].Vendor===vendor&&value[i].Status===status){
        counter++;
        console.log(counter);
      }
    }
    return counter;
    },

    Calculated(resp){
      this.response=resp;
    },
  }
}
</script>

<style scoped>
.value {
  text-align: left;
  font-family: Arial, Helvetica, Verdana, sans-serif;
  font-size: 150%;
  font-variant: small-caps;
  font-weight: lighter;
  box-shadow: 0 3px 15px #9555a5;
  background-color: #82be82;
}
.value-over {
  width: 15px 10px;
  background-color: #9555a5;
  text-align: center;
}
.vendor-block{
  margin: 0.5em;
}
</style>