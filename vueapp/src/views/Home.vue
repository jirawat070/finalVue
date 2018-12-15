<template>
    <div>
        <h1> List</h1>
        <b-table striped hover 
        :items="suppliers" 
        :fields="fields" 
        :per-page="pageSize" 
        :current-page="pageIndex"></b-table>
        <b-pagination size="md" :total-rows="suppliers.length" v-model="pageIndex" :per-page="pageSize">
    </b-pagination>
    </div>
</template>
<script>
import axios from 'axios'
export default {
  name: 'suppliers',
  data(){
      return {
          message:'Project 2',
          suppliers: [],
          pageSize: 10,
          pageIndex: 1,
          fields: [ 
              {
                  key:'SupplierID',
                  sortable : true
              },
              {
                  key:'CompanyName',
                  sortable : true
              },
              {
                  key:'ContactName',
                  sortable : true,
                  
              },
                {
                  key:'ContactTitle',
                  sortable : true,
                  
              }
        ],
      }
  },
  mounted(){
      var instance = this
      axios
      .get('https://shielded-spire-43023.herokuapp.com/api/products/')
      .then(function(response){
          console.log(response.data)
          instance.suppliers = response.data.data
      })
  }
}
</script>
