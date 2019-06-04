<template>
  <div>
    <p>Home Page</p>
    <p>Random Number from backend: {{ randomNumber }}</p>
    <button @click="getRandom">New Random Number</button>
  </div>
</template>


<script>
import axios from 'axios'
export default{
  data() {
    return{
      randomNumber: 0
    }
  },
  methods: {
    getRandom(){
      this.randomNumber = this.getRandomFromBackend()
    },
    getRandomFromBackend(){
      const path = 'http://appdemo-lb-698580653.eu-west-2.elb.amazonaws.com/api/random'
      axios.get(path)
        .then(response => {
          this.randomNumber = response.data.randomNumber
        })
        .catch(error => {
          console.log(error)
        })
    }
  },
  created(){
    this.getRandom()
  }
}
</script>
