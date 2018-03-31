<template>
  <div class="container">
    <div class="row">
      <div class="col-md-8  col-md-offset-2">
        <h1 class="center">Http Request Sample  </h1>
        <div class="row">
          <div class = 'form-group col-md-6 float-left' >

            <input v-model="user.username"  placeholder="Enter Name" class="form-control" type="text"/>
          </div>
        </div>

      <div class="row">
        <div class = 'form-group col-md-6 float-right'>

          <input v-model="user.email" placeholder="Enter Email" class="form-control" type="text"/>
        </div>
      </div>

        <div class="row">
          <div class = 'form-group col-md-6 float-right'>
            <button @click="submit" class="btn btn-secondary btn-block col-md-6"> Submit Data</button>
          </div>
        </div>

        <div class="row">
          <div class = 'form-group col-md-6 float-right'>
            <button @click="fetchData" class="btn btn-secondary btn-block col-md-6"> Get Data</button>
          </div>
        </div>
        <hr class="col-md-6"/>
        <ul class="list-group" style="text-align:center" >
          <li class="list-group-item" v-for="u in users">Name: {{ u.username}}, Email: {{u.email}}</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script type="text/javascript">
  export default {
    data ()
    {
      return {
        user: {
          username: '',
          email: ''
        },
        users: []
      };
    },
    methods: {
      submit(){
        this.$http.post('https://morgyken-5e26f.firebaseio.com/data.json', this.user)
          .then(response => {
            alert('Data was inserted Successfully')
          },
            error=> { console.log(error)})
      },
      fetchData(){
        this.$http.get('https://morgyken-5e26f.firebaseio.com/data.json')
          .then(response => {
            return response.json();
            alert('Data fetch successful');
        }).then(data => {
          const resultArray = [];
          for(let key in data)
          {
            resultArray.push(data[key]);
          }
          this.users = resultArray;
        });
      }
    }
  }
</script>

<style>
</style>
