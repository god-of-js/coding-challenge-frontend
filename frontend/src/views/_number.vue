<template>
  <div class="home">
    <header>Call logs of {{ agent.firstName + " " + agent.lastName }}</header>
    <table>
      <tr v-for="(log, index) in agent.logs" :key="index">
        <td class="user-container">
          <div class="avatar">
            <img
              :src="agent.photo"
              :alt="agent.firstName + ' ' + agent.lastName"
            />
          </div>
          <router-link :to="`/agent/${agent.identifier}`" class="link">{{
            agent.firstName + " " + agent.lastName
          }}</router-link>
        </td>
        <td>
          <router-link :to="`/call/${log.number}`" class="link">{{
            log.number
          }}</router-link>
        </td>
        <td>{{ new Date(log.dateTime).toLocaleString() }}</td>
        <td>{{ log.resolutions.resolution }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
import { mapState } from "vuex";
export default {
  name: "Home",
  computed: {
    ...mapState(["agent"]),
  },
  
  mounted() {
    this.$store.dispatch("getAgentByNumber", this.$route.params.number);
  },
  methods: {},
};
</script>

<style lang="scss" scoped>
.home {
  width: 60%;
  margin: auto;
  margin-top: 25px;
  text-align: left;
  header {
    padding: 9px;
    text-align: left;
    font-weight: bold;
    background: #f1f1f1;
    margin-bottom: 9px;
  }
  table {
    width: 100%;
    .user-container {
      display: flex;
      padding: 5px;
      align-items: center;
    }
  }
  img {
    width: 50px;
    height: 50px;
    border-radius: 50%;
    margin-right: 10px;
  }
  .link {
    text-decoration: none;
    font-weight: bold;
  }
}
</style>
