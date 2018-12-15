<template>
 <b-row>
   
      <b-col md="6" class="my-1">
        <b-form-group horizontal label="Filter" class="mb-0">
          <b-input-group>
            <b-form-input v-model="filter" placeholder="Type to Search" />
            <b-input-group-append>
              <b-btn :disabled="!filter" @click="filter = ''">Clear</b-btn>
            </b-input-group-append>
          </b-input-group>
        </b-form-group>
      </b-col>


  <b-table striped hover :items="suppliers" :fields="fields" :filter="filter" :per-page="pageSize" :current-page="pageIndex">
    <template slot="show_details" slot-scope="row">
      <!-- we use @click.stop here to prevent emitting of a 'row-clicked' event  -->
      <b-button size="sm" @click.stop="row.toggleDetails" class="mr-2">
       {{ row.detailsShowing ? 'Hide' : 'Show'}} Details
      </b-button>
      <!-- In some circumstances you may need to use @click.native.stop instead -->
      <!-- As row.showDetails is one-way, we call the toggleDetails function on @change -->
     
    </template>
    <template slot="row-details" slot-scope="row">
      <b-card>
        <b-row class="mb-2">
          <b-col sm="3" class="text-sm-right"><b>supplier_id:</b></b-col>
          <b-col>{{ row.item.supplier_id }}</b-col>
        </b-row>
        <b-row class="mb-2">
          <b-col sm="3" class="text-sm-right"><b>company_name:</b></b-col>
          <b-col>{{ row.item.company_name }}</b-col>
        </b-row>
        <b-row class="mb-2">
          <b-col sm="3" class="text-sm-right"><b>contact_name:</b></b-col>
          <b-col>{{ row.item.contact_name }}</b-col>
        </b-row>
        <b-row class="mb-2">
          <b-col sm="3" class="text-sm-right"><b>contact_title:</b></b-col>
          <b-col>{{ row.item.contact_title }}</b-col>
        </b-row>
        <b-row class="mb-2">
          <b-col sm="3" class="text-sm-right"><b>address:</b></b-col>
          <b-col>{{ row.item.address }}</b-col>
        </b-row>
        <b-row class="mb-2">
          <b-col sm="3" class="text-sm-right"><b>city:</b></b-col>
          <b-col>{{ row.item.city }}</b-col>
        </b-row>
        <b-row class="mb-2">
          <b-col sm="3" class="text-sm-right"><b>region:</b></b-col>
          <b-col>{{ row.item.region }}</b-col>
        </b-row>
        <b-row class="mb-2">
          <b-col sm="3" class="text-sm-right"><b>postal_code:</b></b-col>
          <b-col>{{ row.item.postal_code }}</b-col>
        </b-row>
          <b-row class="mb-2">
          <b-col sm="3" class="text-sm-right"><b>country:</b></b-col>
          <b-col>{{ row.item.country }}</b-col>
        </b-row>
           <b-row class="mb-2">
          <b-col sm="3" class="text-sm-right"><b>phone:</b></b-col>
          <b-col>{{ row.item.phone }}</b-col>
        </b-row>
        <b-row class="mb-2">
          <b-col sm="3" class="text-sm-right"><b>fax:</b></b-col>
          <b-col>{{ row.item.fax }}</b-col>
        </b-row>
         <b-row class="mb-2">
          <b-col sm="3" class="text-sm-right"><b>homepage:</b></b-col>
          <b-col>{{ row.item.homepage }}</b-col>
        </b-row>
        <b-button size="sm" @click="row.toggleDetails">Hide Details</b-button>
      </b-card>
    </template>
  </b-table>
   <b-col md="6" class="my-1">
  <b-pagination align="center" size="md" :total-rows="suppliers.length" v-model="pageIndex" :per-page="pageSize">
    </b-pagination> 
     </b-col>
    <br>
 <b-col md="6" class="my-1">
    <div>CurrentPage: {{pageIndex}}</div>  
     </b-col>
  </b-row>
</template>

    

<script>

import axios from 'axios'
export default {
  name: 'suppliers',
  data(){
      return {
          message:'Final',
          suppliers: [],
          pageSize: 10,
          filter: null,
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
                   key:  'show_details'  
              } 
               
        ],
      }
  },
  computed: {
    sortOptions () {
      // Create an options list from our fields
      return this.fields
        .filter(f => f.sortable)
        .map(f => { return { text: f.label, value: f.key } })
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
