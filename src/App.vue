<template>
  <div id="main-app" class="container">
    <div class="row justify-content-center">
      <add-appointment/>
      <appointment-list v-bind:appointments="appointments" @remove="removeItem" @edit="editItem" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import AppointmentList from "./components/AppointmentList";
import AddAppointment from "./components/AddAppointment";
import _ from "lodash";
export default {
  name: "MainApp",
  data: function() {
    return {
      title: "Appointment List",
      appointments: [],
      aptIndex: 0
    };
  },
  components: {
    AppointmentList,
    AddAppointment
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
  methods: {
    removeItem: function(apt) {
      return (this.appointments = _.without(this.appointments, apt));
    },
    editItem: function(id, field, text) {
      const aptIndex = _.findIndex(this.appointments, {aptId: id}); this.appointments[aptIndex] [field] = text;
    }
  }
};
</script>