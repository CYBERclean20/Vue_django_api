<template>
  <div>
    <v-container>
      <form @submit.prevent="onSubmit">
        <v-calendar v-model="recording_date"></v-calendar>
        <!-- <v-text-field
          v-model="recording_date"
          label="測定日"
          required
        ></v-text-field> -->
        <v-text-field
          v-model="moningbody_temperature"
          label="朝の体温"
          required
        ></v-text-field>
        <v-text-field
          v-model="moningbody_condition"
          label="朝の体調"
        ></v-text-field>
        <v-text-field
          v-model="nightbody_temperature"
          label="夜の体温"
        ></v-text-field>
        <v-text-field
          v-model="nightbody_condition"
          label="夜の体調"
        ></v-text-field>
        <v-text-field v-model="etc" label="備考"></v-text-field>
        <div class="text-center">
          <v-btn color="success" type="submit">送信</v-btn>
        </div>
      </form>
    </v-container>
  </div>
</template>

<script>
import { apiService } from "../common/api.service.js";

export default {
  name: "JobEditor",
  props: {
    id: {
      type: Number,
      required: false,
    },
  },
  data() {
    return {
      recording_date: null,
      moningbody_temperature: null,
      moningbody_condition: null,
      nightbody_temperature: null,
      nightbody_condition: null,
      etc: null,
      error: null,
    };
  },
  methods: {
    onSubmit() {
      let endpoint = "/api/jobs/";
      let method = "post";
      console.log("1");
      if (this.id !== undefined) {
        endpoint += this.id + "/";
        method = "PUT";
      }
      apiService(endpoint, method, {
        recording_date: this.recording_date,
        moningbody_temperature: this.moningbody_temperature,
        moningbody_condition: this.moningbody_condition,
        nightbody_temperature: this.nightbody_temperature,
        nightbody_condition: this.nightbody_condition,
        etc: this.etc,
        error: null,
      }).then((job_data) => {
        console.log("2");
        this.$router.push({
          name: "job",
          params: { id: job_data.id },
        });
      });
    },
  },
  async beforeRouterEnter(to, from, next) {
    console.log("###");
    if (to.params.id != undefined) {
      console.log(to.params.id);
      let endpoint = "/api/jobs/" + to.params.id + "/";
      let data = await apiService(endpoint);
      return next((vm) => {
        (vm.recording_date = data.recording_date),
          (vm.moningbody_temperature = data.moningbody_temperature),
          (vm.moningbody_condition = data.moningbody_condition),
          (vm.nightbody_temperature = data.nightbody_temperature),
          (vm.nightbody_condition = data.nightbody_condition),
          (vm.etc = data.etc);
      });
    } else {
      return next();
    }
  },
  created() {
    document.title = "Editor - Job";
  },
};
</script>
