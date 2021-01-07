<template>
  <div class="calculator">
    <div class="calculator__header"> Реестр активных элементов </div>
    <div class="calculator__content">
      <div class="calculator__column1">
        <label>Филиал </label>
        <select v-model="branchesSelected">
          <option v-for="branch in branches" v-bind:key="branch.branchCode" v-bind:value="branch.branchCode">
            {{ branch.branchName }}
          </option>
        </select>
      </div>
      <div class="calculator__list" v-if="branchesSelected != 0">
      <div class="calculator__column2">
        <label>Регион </label>
        <select v-model="regionsSelected">
          <option v-for="region in regions" v-bind:key="region.code" v-bind:value="region.code">
            {{ region.name }}
          </option>
        </select>
      </div>
      </div>
    </div>
    <div class="calculator__actions">
      <button v-on:click="onShow">Показать</button>
    </div>
    <hr>
  </div>
</template>


<script>
export default {
  data() {
    return {
      branches: [],
      branchesSelected: 0,
      regionsSelected: 0,
      result: [],
      apiResp: []
    }
  },

  computed: {
    regions() {
      let findedBranch = this.branches.find(branch =>this.branchesSelected === branch.branchCode );
      if (findedBranch) {
        return findedBranch.regions;
      } else {
        return [];
      }
    }
  },

  methods: {
    onShow() {
      let response = this.getObjectsByRegionCode(this.regionsSelected)
      this.$emit('calculated', response);
    },

    getBranchesAndRegions () {
      return [
        {
          branchCode: 'CN',
          branchName: 'Центральный филиал',
          regions: [
            {name: 'Брянская область', code: 32},
            {name: 'Владимирская область', code: 33},
            {name: 'Калужская область', code: 40},
            {name: 'Курская область', code: 46},
          ]
        },
        {
          branchCode: 'KV',
          branchName: 'Кавказский филиал',
          regions: [
            {name: 'Республика Адыгея', code: 1},
            {name: 'Республика Дагестан', code: 5},
            {name: 'Краснодарский край', code: 23},
            {name: 'Воронежская область', code: 36},
          ]
        }
      ]
    },

    getObjectsByRegionCode (region) {
      let apiResponse = [
        { 
          Vendor:"HUAWEI",
          RegionsCode: 5,
          Status:"ACTIVE"
        },        { 
          Vendor:"HUAWEI",
          RegionsCode: 32,
          Status:"DISABLE"
        },
                { 
          Vendor:"HUAWEI",
          RegionsCode: 33,
          Status:"ACTIVE"
        },
                { 
          Vendor:"HUAWEI",
          RegionsCode: 40,
          Status:"DISABLE"
        },
                { 
          Vendor:"NOKIA",
          RegionsCode: 46,
          Status:"DISABLE"
        },
                { 
          Vendor:"ZTE",
          RegionsCode: 46,
          Status:"ACTIVE"
        },
                { 
          Vendor:"ZTE",
          RegionsCode: 5,
          Status:"DISABLE"
        },
                { 
          Vendor:"ZTE",
          RegionsCode: 23,
          Status:"DISABLE"
        },
                { 
          Vendor:"HUAWEI",
          RegionsCode: 36,
          Status:"ACTIVE"
        },
                { 
          Vendor:"NOKIA",
          RegionsCode: 32,
          Status:"ACTIVE"
        },
                { 
          Vendor:"HUAWEI",
          RegionsCode: 33,
          Status:"DISABLE"
        },
                { 
          Vendor:"NOKIA",
          RegionsCode: 40,
          Status:"DISABLE"
        },
                { 
          Vendor:"ZTE",
          RegionsCode: 1,
          Status:"DISABLE"
        },
                { 
          Vendor:"NOKIA",
          RegionsCode: 23,
          Status:"ACTIVE"
        },
                { 
          Vendor:"HUAWEI",
          RegionsCode: 36,
          Status:"ACTIVE"
        },
                { 
          Vendor:"NOKIA",
          RegionsCode: 33,
          Status:"ACTIVE"
        },
                { 
          Vendor:"ZTE",
          RegionsCode: 5,
          Status:"ACTIVE"
        },
                { 
          Vendor:"HUAWEI",
          RegionsCode: 5,
          Status:"ACTIVE"
        },
                { 
          Vendor:"ZTE",
          RegionsCode: 40,
          Status:"ACTIVE"
        },
                { 
          Vendor:"ZTE",
          RegionsCode: 46,
          Status:"ACTIVE"
        },
      ]

      let response = [];
      for(let i=0;i<apiResponse.length;i++){
        if(apiResponse[i].RegionsCode==region){
          response.push(apiResponse[i]);
        }
      }
      return response
    },
  },

  created() {
    this.branches = this.getBranchesAndRegions();
  }
}
</script>

<style>
.calculator {
  font-family: Arial, Helvetica, Verdana, sans-serif;
  font-size: 150%;
  font-variant: small-caps;
  font-weight: lighter;
  box-shadow: 0 3px 15px #9555a5;
  background-color: #82be82;
  text-align: center;
}
.calculator__header {
  width: 150px 10px;
  background-color: #9555a5;
  text-align: center;
}
</style>