<template>
  <div class="col-12">
    <div class="card textcenter mt-3">
      <div class="card-header bg-primary text-white"
      @click="hidepanel=!hidepanel">
        <font-awesome-icon icon="plus" class="mr-3" />Add Appointment
      </div>
    </div>
    <!-- panel-heading -->

    <div class="panel-body" v-bind:class="{'d-none': hidepanel}">
      <form class="add-appointment form-horizontal" 
        @submit.prevent="requestAdd">
        <div class="form-group">
          <label class="col-sm-2 control-label" for="petName">Pet Name</label>
          <div class="col-sm-10">
            <input type="text" class="form-control" id="petName" placeholder="Pet's Name"
              v-model="formData.petName" />
          </div>
          <!-- col-sm-10 -->
        </div>
        <!-- form-group -->

        <div class="form-group">
          <label class="col-sm-2 control-label" for="petOwner">Pet Owner</label>
          <div class="col-sm-10">
            <input type="text" class="form-control" id="petOwner" placeholder="Owner's Name" 
              v-model="formData.ownerName"/>
          </div>
          <!-- col-sm-10 -->
        </div>
        <!-- form-group -->

        <div class="form-group">
          <label class="col-sm-2 control-label" for="aptDate">Date</label>
          <div class="col-sm-4">
            <input type="date" class="form-control" id="aptDate" 
              v-model="formData.aptData"/>
          </div>
          <!-- col-sm-4 -->
          <label class="col-sm-2 control-label" for="aptTime">Time</label>
          <div class="col-sm-4">
            <input type="time" class="form-control" id="aptTime" 
              v-model="formData.aptTime"/>
          </div>
          <!-- col-sm-4 -->
        </div>
        <!-- form-group -->

        <div class="form-group">
          <label class="col-sm-2 control-label" for="aptNotes">Apt. Notes</label>
          <div class="col-sm-10">
            <textarea
              class="form-control"
              rows="4"
              cols="50"
              id="aptNotes"
              placeholder="Appointment Notes"
              v-model="formData.aptNotes"
            ></textarea>
          </div>
          <!-- col-sm-10 -->
        </div>
        <!-- form-group -->

        <div class="form-group">
          <div class="col-sm-offset-2 col-sm-10">
            <button type="submit" class="btn btn-primary pull-right">Add Appointment</button>
          </div>
          <!-- col-sm-offset-2 -->
        </div>
        <!-- form-group -->
      </form>
    </div>
    <!-- panel-body -->
  </div>
  <!-- panel-primary -->
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
export default {
  name: "AddAppointment",
  data() {
    return {
      formData: [],
      hidepanel: true
    };
  },
  components: {
    FontAwesomeIcon
  },
  methods: {
    requestAdd: function() {
      this.formData = {
        petName: this.formData.petName,
        petOwner: this.formData.ownerName,
        aptDate: this.formData.aptData + ' ' + this.formData.aptTime,
        aptNotes: this.formData.aptNotes,
      };
      this.$emit("add", this.formData);
      this.formData=[];
      this.hidepanel = true;
    }
  }
};
</script>

<style lang="css" scoped>
.card-header {
  cursor: pointer;
}
</style>