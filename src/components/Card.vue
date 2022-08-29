<template>
    
    <div class="container text-center p-4">
        <h2 class="text-primary">GitHub Status</h2>
        <div class="row">
            <div>
                <ul class="col-8 offset-2 list-group fs-2" v-for="info in infos" :key="info.id">
                    <li class="list-group-item m-2 bg-light">{{info.name}} 
                        <span class="badge bg-success rounded-pill text-capitalize" v-if="info.status === 'operational'">{{info.status}}</span>
                        <span class="badge bg-danger rounded-pill text-capitalize" v-else >{{info.status}}</span>
                    </li>
                </ul>
            </div>
        </div>
        <button class="btn btn-outline-primary btn-lg" @click="apiFetch">Refresh Status</button>

    </div>
</template>

<script>
export default {

  data () {
    return {
      infos: null
    }
  },
  methods:{
     apiFetch(){
         fetch(`https://www.githubstatus.com/api/v2/summary.json`)
    .then(response => response.json())
    .then((data) => {
        console.log(data);
        this.infos = data.components;
      })
    }
    }, 
  mounted () {
      this.apiFetch();
    }
}
</script>