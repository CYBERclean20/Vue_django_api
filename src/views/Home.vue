<template>
  <div>
    <v-container>
      <div v-for="job of jobs" :key="job.pk">
        <h2>
          <router-link :to="{ name: 'job', params:{ id: job.id } }"
            class="job-link">
            {{ job.company_name }}
          </router-link>
        </h2>
        <p>{{ job.job_title }}</p>
        <hr>
      </div>
    </v-container>
  </div>
</template>

<script>
// @ is an alias to /src
import { apiService } from '../common/api.service.js'

export default {
  name: "Home",
  data() {
    return {
      jobs: []
    };
  },
  methods: {
    getJobs() {
      
      let endpoint = 'api/jobs/'
      apiService(endpoint).then(data => {
        console.log(data);
        this.jobs.push(...data);
      });
    }
  },
  created(){
    this.getJobs();
    document.title = 'Job Board';
  },
};
</script>
<style scoped>
  .job-link{
    font-weight: bold;
    color:black;
    text-decoration: none;
  }

  .job-link:hover{
    color:#41B883;
  }
</style>