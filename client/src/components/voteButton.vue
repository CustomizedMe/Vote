<template>
  <div class="main">
    <div class="head">Hi, {{ name || "" }}</div>
            <div class="subhead"> Current Vote : {{btn}} </div>                                                                                                        
  <button @click="changeVote" class="btn">Change Vote</button></div> 
  </div>
</template>

<script>
import axios from "axios"
export default {
  name: "voteButton",
  data: function() {
    return {
      name: "",
      voted: false,
    }
  },
  methods: {
    async changeVote() {
      const res = await fetch("/api/vote/toggle", {
        method: "PUT",
        headers: {
          "Content-Type": "application/json",
        },
      }).catch((error) => {
        console.log(error)
      })
      const data = await res.json()
      console.log("data", data)
      window.location.reload()
    },
  },
  async created() {
    try {
      const res = await axios.get(`/api/auth/me`)
      if (!res.data) this.$router.push({ path: "/" })
      else {
        this.name = res.data.name
        this.voted = res.data.voted
      }
    } catch (e) {
      console.error(e)
    }
  },
  computed: {
    btn() {
      return this.voted ? "Vote out" : "I am chill"
    },
  },
}
</script>

<style lang="scss">
.main{
  margin-top:4rem
}
.head {
  font-size: 1.5rem;
  font-weight: 600;
  color: white;
  margin-bottom: .3em;
}
.subhead {
  color: #42b983;
  font-size: 1.2rem;
  margin-bottom: .75em;
}
.btn {
  color: #42b983;
  font-size: 1.2rem;
  border: 2px solid #42b983;
  border-radius: 5px;
  background: none;
  cursor: pointer;
  color: #42b983;
}
</style>
