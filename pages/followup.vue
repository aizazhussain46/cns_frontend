<template>
  <v-data-table
    :headers="headers"
    :items="data"
    sort-by="followup"
    class="elevation-1"
  >
    <template v-slot:top>
      <v-toolbar flat color="white">
        <v-toolbar-title>Follow Ups</v-toolbar-title>        
      </v-toolbar>
    </template>
    
    <template v-slot:no-data>
      <v-btn color="primary" @click="initialize">Reset</v-btn>
    </template>
  </v-data-table>
</template>

<script>
  export default {
    data: () => ({
      dialog: false,
      headers: [
        {
          text: 'id',
          sortable: true,
          value: 'id',
        },
        {
          text: 'Field Officer',
          sortable: true,
          value: 'field officer',
        },
        {
          text: 'Patient',
          sortable: true,
          value: 'patient',
        },
        {
          text: 'Visit',
          sortable: false,
          value: 'visits',
        },
        {
          text: 'Date',
          sortable: false,
          value: 'created_at',
        },
        

      ],
      data: [],
      defaultItem: {
       field_officer_id:'',
       patient:'',
       visits:'',
       created_at:'',
      },
    }),

    computed: {
      formTitle () {
        return this.editedIndex === -1 ? 'New Item' : 'Edit Item'
      },
    },

    watch: {
      dialog (val) {
        val || this.close()
      },
    },

    created () {
      this.initialize()
    },

    methods: {
      initialize () {

      this.$axios.get('followup').then(res => {

          this.data = res.data.data 

        });

      },


      
    },
  }
</script>