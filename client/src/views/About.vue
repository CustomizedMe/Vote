<template>
  <div class="about">
    <voteButton />
    <VoteList />
  </div>
</template>
<script>
import voteButton from "../components/voteButton"
import VoteList from "../components/VoteList.vue"
export default {
  name: "About",
  components: { voteButton, VoteList },
}
</script>
