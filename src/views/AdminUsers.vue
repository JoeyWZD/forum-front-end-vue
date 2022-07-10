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
const dummyData = {
  users: [
    {
      id: 1,
      name: "root",
      email: "root@example.com",
      password: "$2a$10$NaFxxKY/enRJ7qMRQafrK.4pWvCRLWHZft5m2Z3znhKV/amCvJPwm",
      isAdmin: true,
      image: null,
      createdAt: "2022-04-24T01:28:16.000Z",
      updatedAt: "2022-04-24T01:28:16.000Z",
    },
    {
      id: 2,
      name: "user1",
      email: "user1@example.com",
      password: "$2a$10$wW0J2C.uUY80yJ3oX0i11.vrMEMhqZ3ufqabZXfjzwvbwyGfeVlS2",
      isAdmin: false,
      image: null,
      createdAt: "2022-04-24T01:28:16.000Z",
      updatedAt: "2022-04-24T01:28:16.000Z",
    },
    {
      id: 3,
      name: "user2",
      email: "user2@example.com",
      password: "$2a$10$DGliZ2sx9n0NMLxjkBtH0eASt0XW2uyaTWkTbGyXvHW/jahQE.0Cq",
      isAdmin: false,
      image: null,
      createdAt: "2022-04-24T01:28:16.000Z",
      updatedAt: "2022-04-24T01:28:16.000Z",
    },
  ],
};

const dummyUser = {
  currentUser: {
    id: 1,
    name: "管理者",
    email: "root@example.com",
    image: "https://i.pravatar.cc/300",
    isAdmin: true,
  },
  isAuthenticated: true,
};
import AdminNav from "./../components/AdminNav.vue";
export default {
  components: {
    AdminNav,
  },
  data() {
    return {
      users: [],
      currentUser: {},
    };
  },
  created() {
    this.fetchUser();
  },
  methods: {
    fetchUser() {
      this.currentUser = dummyUser.currentUser;
      this.users = dummyData.users;
    },
    // toggleUserRole(userId) {
    //   this.users = this.users.map( user => {
    //     if (user.id === userId) {
    //       return {
    //         ...user,
    //         isAdmin: !user.isAdmin,
    //       }
    //     }
    //     return user
    //   })
    // }
    toggleUserRole(userId) {
      const user = this.users.find((user) => user.id === userId);
      user.isAdmin = !user.isAdmin;
    },
  },
};
</script>