<template>
  <div>
    <v-container>
      <v-row>
        <v-col cols="10">
          <v-data-table
          :headers="headers"
          :items="jobs"
          disable-paginationprop
          :server-items-length="total"
          :loading="loading"
         
          locale="ja-jp"
          loading-text="読込中"
          no-data-text="データがありません。"
          @click:row="clickRow"
      >
          
      
        <!-- <thead class="thead-dark">
          <tr>
            <th>Data</th>
            <th>Moning Temp</th>
            <th>Night Temp</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="job of jobs" :key="job.pk">
              <td><router-link :to="{ name: 'job', params:{ id: job.id } }"
            class="job-link">{{ job.recording_date }}</router-link></td>
              <td><router-link :to="{ name: 'job', params:{ id: job.id } }"
            class="job-link">{{ job.moningbody_temperature }}</router-link></td>
              <td><router-link :to="{ name: 'job', params:{ id: job.id } }"
            class="job-link">{{ job.nightbody_temperature }}</router-link></td>
          </tr>
        </tbody> -->
      </v-data-table>
    </v-col>
  </v-row>
        
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
import 'vue-good-table/dist/vue-good-table.css'

export default {
  name: "Home",
  el:'#app',
  data() {
    return {
      headers: [
          { 
            text: 'Date', 
            value: 'recording_date' 
          },
          {
            text: 'Moning Temp',
            value: 'moningbody_temperature',
          },
          { text: 'Night Temp', 
            value: 'nightbody_temperature' 
          },
        ],
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
    },
    clickRow: function(item) {
      // const selected = this.items.indexOf(item);
      // alert((selected + 1) + "行目をクリックしました。");
      this.$router.push({
          name: "job",
          params: { id: item.id },
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
 
 /* .table { 
   background-color: #41B883;
 } */
</style>
