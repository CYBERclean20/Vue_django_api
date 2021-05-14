<template>
  <div>
    <v-container>
      <h2 class="mb-5">{{ job.recording_date }}</h2>
      <p>朝の体温: {{ job.moningbody_temperature }}</p>
      <p>朝の体調: {{ job.moningbody_condition }}</p>
      <p>夜の体調: {{ job.nightbody_temperature }}円</p>
      <p>夜の体調: {{ job.nightbody_condition }}</p>
      <p>気になること: {{ job.etc }}</p>
    </v-container>
  </div>
</template>
<script>

import { apiService } from '../common/api.service.js'

export default{
  name: 'job',
  props: {
    id: {
      type: Number,
      required: true
    } 
  },
  data() {
    return {
      job: {}
    }
  },
  methods: {
   
    setPageTitle(title){
      document.title = title;
    },
    
    getJobData() {
      console.log("ffff");
      let endpoints = '/api/jobs/'+this.id+'/';
      apiService(endpoints).then(data => {
        console.log("ff");
        this.job = data;//.replace(/\\n/g, "\\n").replace(/\\'/g, "\\'").replace(/\\"/g, '\\"').replace(/\\&/g, "\\&").replace(/\\r/g, "\\r").replace(/\\t/g, "\\t").replace(/\\b/g, "\\b").replace(/\\f/g, "\\f");
        // console.log(this.job);
        // console.log(this.job[this.id]);
        this.serPageTitle(data.company_name);
      })
    }
  },
  created(){
    this.getJobData();
  }
}
</script>
