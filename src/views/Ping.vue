<template>
  <div>
    <p>{{ msg }}</p>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Ping',
  data() {
    return {
      msg: ''
    }
  },
  methods: {
    getMessage() {
      const path = 'http://localhost:5000/ping'
      axios.get(path)
        .then(res => {
          this.msg = res.data
          console.log(`response: ${this.msg}`);
        })
        .catch(err => {
          console.log(err)
        })
    },
  },
  created() {
    this.getMessage()
  },
}
</script>
