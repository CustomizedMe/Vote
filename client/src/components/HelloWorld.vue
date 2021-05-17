<template>
  <div class="hello">
    <div class="cover">
      <div class="head">
        Has the monitor written your name on blackboard, in teacher's absence,
        without any reason?
      </div>
      <div class="subhead">
        Login with Google Id so that we can come together and vote out the
        current class monitor
      </div>
      <div class="login">
        <GoogleLogin
          :params="params"
          :renderParams="renderParams"
          :onSuccess="onSuccess"
          :onFailure="onFailure"
          class="login"
        ></GoogleLogin>
      </div>

      <div>
        <button @click="userLogout" class="logout">
          <GoogleLogin :params="params" :logoutButton="true" class="logout-btn"
            >Logout</GoogleLogin
          >
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import GoogleLogin from "vue-google-login"
import axios from "axios"
export default {
  name: "HelloWorld",
  components: {
    GoogleLogin,
  },
  data() {
    return {
      params: {
        client_id: "216261352964-k9redj02olcjfkl0toovmfec26k3sdm0",
      },
      renderParams: {
        width: 400,
        height: 50,
        longtitle: true,
      },
    }
  },
  methods: {
    async userLogout() {
      const res = await axios.delete(`/api/auth/logout`)
      const message = res.data.msg
      alert(message)
    },
    onFailure(googleUser) {
      alert("Something went wrong")
    },
    async onSuccess(googleUser) {
      const res = await fetch("/api/auth/googlelogin", {
        method: "POST",
        body: JSON.stringify({
          token: googleUser.qc.id_token,
        }),
        headers: {
          "Content-Type": "application/json",
        },
      })
      const data = await res.json()
      this.$router.push({ path: "/about" })
    },
  },
}
</script>

<style lang="scss">
h3 {
  margin: 40px 0 0;
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
.hello {
  display: flex;
  align-items: center;
  // margin: auto;
  // border: #42b983 20px solid;
  flex-direction: column;
  justify-content: center;
}
.login {
  margin: 2rem 0rem;
  align-self: center;
  display: flex;
  justify-content: center;
}
.cover {
  margin-top: 4rem;
}
.head {
  font-size: 1.5rem;
  font-weight: 600;
  color: white;
}
.subhead {
  color: #42b983;
  font-size: 1.2rem;
}
.logout-btn {
  border: none;
  background: none;
  color: #42b983;
  cursor: pointer;
}
.logout {
  color: #42b983;
  font-size: 1.2rem;
  border: 2px solid #42b983;
  border-radius: 5px;
  background: none;
  cursor: pointer;
  color: #42b983;
}
</style>
