<template>
  <main>
    <div class="app p-4 container-fluid">
      <div class="row">
        <div class="col col-md-4 mt-4 offset-md-4">
          <div class="text-center">
            <div v-if="user">
              <UserCard :user="user"></UserCard>
              <button
                type="button"
                @click="fetchUser"
                class="btn btn-primary btn-lg btn-block mt-2"
              >
                Fetch New User
              </button>
            </div>
            <div v-else class="text-center">
              <div class="spinner-border spinner-grow" role="status"></div>
              <div class="text-white">Loading...</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import axios from "axios";
import UserCard from "./components/UserCard.vue";

export default {
  name: "App",
  data() {
    return {
      user: null,
    };
  },
  components: { UserCard },
  mounted() {
    this.fetchUser();
  },
  methods: {
    fetchUser: function () {
      axios
        .get("https://randomuser.me/api/")
        .then((response) => {
          this.user = response.data.results[0];
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>

<style>
.card {
  margin-top: 125px;
}
.img {
  margin-top: -80px;
}
</style>
