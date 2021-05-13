<template>
  <div>
    <v-container>
      <h2 class="mb-5">{{ job.company_name }}</h2>
      <p>職種: {{ job.job_title }}</p>
      <p>内容: {{ job.job_description }}</p>
      <p>給料: {{ job.salary }}円</p>
      <p>都道府県: {{ job.prefectures }}</p>
      <p>市町村: {{ job.city }}</p>
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
