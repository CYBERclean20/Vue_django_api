<template>
  <div>
    <v-container>
      <table class="vue_tbl">
        <thead>
          <tr>
            <th>Data</th>
            <th>Moning Temp</th>
            <th>Night Temp</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="job of jobs" :key="job.pk">
            <!-- <router-link :to="{ name: 'job', params:{ id: job.id } }"
            class="job-link"> -->
              <td><router-link :to="{ name: 'job', params:{ id: job.id } }"
            class="job-link">{{ job.recording_date }}</router-link></td>
              <td><router-link :to="{ name: 'job', params:{ id: job.id } }"
            class="job-link">{{ job.moningbody_temperature }}</router-link></td>
              <td><router-link :to="{ name: 'job', params:{ id: job.id } }"
            class="job-link">{{ job.nightbody_temperature }}</router-link></td>
            <!-- </router-link> -->
          </tr>
        </tbody>
      </table>
      <!-- <div v-for="job of jobs" :key="job.pk">
        <h2>
          <router-link :to="{ name: 'job', params:{ id: job.id } }"
            class="job-link">
            {{ job.company_name }}
          </router-link>
        </h2>
        <p>{{ job.job_title }}</p>
        <hr>
      </div> -->
    </v-container>
  </div>
</template>

<script>
// @ is an alias to /src
import { apiService } from '../common/api.service.js'

export default {
  name: "Home",
  el:'#app',
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

  .container {
  height: 100%;
  width: 100%;
  padding: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
  font-family: Arial, Helvetica, sans-serif;
 }
</style>
