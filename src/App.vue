<template>
  <div id="main-app" class="container">
    <div class="row justify-content-center">
      <add-appointment @add="addItem" />
      <search-appointments @searchRecords="searchAppointments"/>
      <appointment-list v-bind:appointments="searchedApts" @remove="removeItem" @edit="editItem" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import AppointmentList from "./components/AppointmentList";
import AddAppointment from "./components/AddAppointment";
import SearchAppointments from "./components/SearchAppointments";
import _ from "lodash";

export default {
  name: "MainApp",
  data: function() {
    return {
      title: "Appointment List",
      appointments: [],
      searchTerms: "",
      aptIndex: 0
    };
  },

  components: {
    AppointmentList,
    AddAppointment,
    SearchAppointments
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
    searchedApts: function() {
      return this.appointments.filter(item => {
        return(
          item.petName.toLowerCase().match(this.searchTerms.toLowerCase()) ||
          item.petOwner.toLowerCase().match(this.searchTerms.toLowerCase()) ||
          item.aptNotes.toLowerCase().match(this.searchTerms.toLowerCase())
        );
      });
    }
  },
  
  methods: {
    removeItem: function(apt) {
      return (this.appointments = _.without(this.appointments, apt));
    },
    editItem: function(id, field, text) {
      const aptIndex = _.findIndex(this.appointments, {aptId: id}); this.appointments[aptIndex] [field] = text;
    },
    addItem: function(apt) {
      apt.aptId = this.aptIndex;
      this.aptIndex++;
      this.appointments.push(apt);
    },
    searchAppointments : function(terms) {
      this.searchTerms = terms;
    }
  }
};
</script>