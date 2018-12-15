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
                  key:'supplier_id',
                  sortable : true
              },
              {
                  key:'company_name',
                  sortable : true
              },
              {
                  key:'contact_name',
                  sortable : true,
                  
              },
                {
                  key:'contact_title',
                  sortable : true,
                  
              },
              {
                  key:'address',
                  sortable : true,
                  
              }
              ,
              {
                  key:'city',
                  sortable : true,
                  
              }
              ,
              {
                  key:'region',
                  sortable : true,
                  
              }
              ,
              {
                  key:'postal_code',
                  sortable : true,
                  
              }
              ,
              {
                  key:'country',
                  sortable : true,
                  
              }
              ,
              {
                  key:'phone',
                  sortable : true,
                  
              }
              ,
              {
                  key:'fax',
                  sortable : true,
                  
              }
              ,
              {
                  key:'homepage',
                  sortable : true,
                  
              }
        ],
      }
  },
  mounted(){
      var instance = this
      axios
      .get('https://frozen-river-13804.herokuapp.com/api/Suppliers')
      .then(function(response){
          console.log(response.data)
          instance.suppliers = response.data.data
      })
  }
}
</script>
