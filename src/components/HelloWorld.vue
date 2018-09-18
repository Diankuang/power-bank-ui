<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
  </div>
</template>

<script>
import qs from 'qs'
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  methods: {
    login () {
      var getVirifyCode = '/api/home/get-verify-code'
      var verifyCode
      this.axios.get(getVirifyCode).then((data) => {
        console.log(data)
        verifyCode = data.data.verifyCode
        if (data.data.code === '0') {
          var login = 'http://localhost:9002/power-bank/home/login'
          var user = {'username': '18676342166', 'password': '123456', 'verifyCode': verifyCode}
          user = qs.stringify(user)
          this.axios.post(login, user, {
            'X-Requested-With': 'XMLHttpRequest',
            'Content-Type': 'application/x-www-form-urlencoded; charset=UTF-8'
          }).then((data) => {
            console.log(data)
          })
        }
      })
    }
  },
  mounted: function () {
    this.login()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
