<template>
  <div id="main-app" class="container">
  <!-- <div class="d-flex"> -->
    <Navbar />
    <div class="row justify-content-center">
      <add-appointment @add="addItem" />
      <search-appointments @searchRecords="searchAppointments" 
        :myKey="filterKey" 
        :myDir="filterDir"
        @requestKey="changeKey"
        @requestDir="changeDir"/>
      <appointment-list v-bind:appointments="filteredApts" 
        @remove="removeItem" 
        @edit="editItem" />
    </div>
  </div>
  <!-- </div> -->
</template>

<script>
import axios from "axios";
import AppointmentList from "./components/AppointmentList";
import AddAppointment from "./components/AddAppointment";
import SearchAppointments from "./components/SearchAppointments";
import Navbar from "./components/Navbar";
import _ from "lodash";

export default {
  name: "MainApp",
  data: function() {
    return {
      title: "Appointment List",
      appointments: [],
      searchTerms: "",
      filterKey: "petName",
      filterDir: "asc",
      aptIndex: 0
    };
  },

  components: {
    AppointmentList,
    AddAppointment,
    SearchAppointments,
    Navbar
  },

  mounted() {
    axios.get("./data/appointments.json").then(
      response =>
        (this.appointments = response.data.map(item => {
          item.aptId = this.aptIndex;
          this.aptIndex++;
          return item;
        }))       
    );
  },

  computed : {
    searchedApts: function() 
    {
      return this.appointments.filter(item => 
      {
        return(
          item.petName.toLowerCase().match(this.searchTerms.toLowerCase()) ||
          item.petOwner.toLowerCase().match(this.searchTerms.toLowerCase()) ||
          item.aptNotes.toLowerCase().match(this.searchTerms.toLowerCase())
        );
      });
    },
    filteredApts: function() 
    {
      return _.orderBy(
        this.searchedApts,
         item => {
           return item[this.filterKey];
           }, 
           this.filterDir
           ); //3 parameters 
    }
  },
  
  methods: {
    removeItem: function(apt) 
    {
      return (this.appointments = _.without(this.appointments, apt));
    },
    editItem: function(id, field, text) 
    {
      const aptIndex = _.findIndex(this.appointments, {aptId: id}); this.appointments[aptIndex] [field] = text;
    },
    addItem: function(apt) 
    {
      apt.aptId = this.aptIndex;
      this.aptIndex++;
      this.appointments.push(apt);
    },
    searchAppointments : function(terms) 
    {
      this.searchTerms = terms;
    },
    changeKey : function(value) {
      this.filterKey = value;
    },
    changeDir : function(value) {
      this.filterDir = value;
    }
  }
};
</script>

<style lang="css" scoped>
/* .container {
    padding-left: 0px;
    margin-left: 0px;
} */
</style>