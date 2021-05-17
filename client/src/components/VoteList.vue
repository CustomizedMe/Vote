<template>
  <div class="main">
    <button @click="openVotes" class="listBtn">List of "Vote Out" votes</button>
    <ul v-if="open">
      <li v-for="vote of votes" :key="vote.id">
        {{ vote.name }} | {{ vote.email }}
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios"

export default {
  name: "VoteList",
  data() {
    return {
      votes: [],
      open: false,
    }
  },
  methods: {
    openVotes() {
      this.open = !this.open
    },
  },
  async created() {
    try {
      const res = await axios.get(`/api/vote/all`)
      this.votes = res.data
    } catch (e) {
      console.error(e)
    }
  },
}
</script>

<style scoped>
ul {
  display: flex;
  flex-direction: column;
}
li {
  list-style: none;
  color: white;
  margin: 2px;
}
.listBtn {
  font-size: 1.2rem;
  border: 2px solid #42b983;
  border-radius: 5px;
  background-color: #42b983;
  color: #0a1128;
  cursor: pointer;
  padding: 4px 8px;
}
</style>
