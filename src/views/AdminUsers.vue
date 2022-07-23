<template>
  <div class="container py-5">
    <!-- AdminNav Component -->
    <AdminNav />
    <table class="table">
      <thead class="thead-dark">
        <tr>
          <th scope="col">#</th>
          <th scope="col">Email</th>
          <th scope="col">Role</th>
          <th scope="col" width="140">Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in users" :key="user.id">
          <th scope="row">
            {{ user.id }}
          </th>
          <td>{{ user.email }}</td>
          <td>{{ user.isAdmin ? "admin" : "user" }}</td>
          <!-- <td>{{ user.role }}</td> -->
          <td>
            <button
              v-if="currentUser.id !== user.id"
              type="button"
              class="btn btn-link"
              @click.stop.prevent="toggleUserRole(user.id)"
            >
              {{ user.isAdmin ? "set as user" : "set as admin" }}
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import adminAPI from "./../apis/admin";
import { Toast } from "./../utils/helpers";
import { mapState } from "vuex";
import AdminNav from "./../components/AdminNav.vue";

export default {
  components: {
    AdminNav,
  },
  data() {
    return {
      users: [],
    };
  },
  created() {
    this.fetchUser();
  },

  computed: {
    ...mapState(["currentUser"]),
  },

  methods: {
    async fetchUser() {
      try {
        const { data } = await adminAPI.getAdminUsers();
        this.userInfo = data.users;
      } catch (error) {
        console.log(error);
        Toast.fire({
          icon: "error",
          title: "請求使用者失敗",
        });
      }
    },

    async toggleUserRole({ userId, isAdmin }) {
      try {
        const { data } = await adminAPI.users.toggleIsAdmin({
          userId,
          isAdmin: (!isAdmin).toString(),
        });
        if (data.status !== "success") {
          throw new Error(data.message);
        }
        this.users = this.users.map((user) => {
          if (user.id === userId) {
            return {
              ...user,
              isAdmin: !isAdmin,
            };
          }
          return user;
        });
      } catch (error) {
        Toast.fire({
          icon: "error",
          title: "無法切換權限，請稍後再試",
        });
      }
    },
  },
};
</script>