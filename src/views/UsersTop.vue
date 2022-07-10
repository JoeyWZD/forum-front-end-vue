<template>
  <div class="container py-5">
    <NavTabs />
    <h1 class="mt-5">美食達人</h1>
    <hr />
    <div class="row text-center">
      <RestaurantsUserTop
        v-for="user in users"
        :key="user.id"
        :initial-user="user"
      />
    </div>
  </div>
</template>

<script>
import NavTabs from "./../components/NavTabs";
import RestaurantsUserTop from "./../components/RestaurantsUserTop.vue";

const dummyUsers = {
  users: [
    {
      id: 1,
      name: "root",
      email: "root@example.com",
      password: "$2a$10$10JUqZOmUsK0LblbEJHaJ.EYvrjkj0ytEPrwvPF4FfDIUjxlBtIZO",
      isAdmin: true,
      image:
        "https://fureverkids.net/wp-content/uploads/2021/04/40150983442_5fc1afe90f_c.jpg?ezimgfmt=ng%3Awebp%2Fngcb1%2Frs%3Adevice%2Frscb1-1",
      createdAt: "2022-07-08T05:38:02.000Z",
      updatedAt: "2022-07-08T05:38:02.000Z",
      Followers: [],
      FollowerCount: 0,
      isFollowed: false,
    },
    {
      id: 2,
      name: "user1",
      email: "user1@example.com",
      password: "$2a$10$SfMkNk.RcqJws7HRD5xl/umoL59oLIVSSv8jfDvCfckLrV05ZdEnO",
      isAdmin: false,
      image:
        "https://fureverkids.net/wp-content/uploads/2021/10/a-black-and-white-tuxedo-or-piebald-cat-kitten-sit-5AN2AT6-1.jpg?ezimgfmt=ng%3Awebp%2Fngcb1%2Frs%3Adevice%2Frscb1-1",
      createdAt: "2022-07-08T05:38:02.000Z",
      updatedAt: "2022-07-08T05:38:02.000Z",
      Followers: [],
      FollowerCount: 0,
      isFollowed: false,
    },
    {
      id: 3,
      name: "user2",
      email: "user2@example.com",
      password: "$2a$10$RIzFHpfPqTjgjUbQDGFksu2ebkPC5QW40GTiwXt6vnFWbNbnCR7OO",
      isAdmin: false,
      image:
        "https://fureverkids.net/wp-content/uploads/2021/10/tabby-cat-sitting-AGZXN9T-1.jpg?ezimgfmt=ng%3Awebp%2Fngcb1%2Frs%3Adevice%2Frscb1-1",
      createdAt: "2022-07-08T05:38:02.000Z",
      updatedAt: "2022-07-08T05:38:02.000Z",
      Followers: [],
      FollowerCount: 0,
      isFollowed: false,
    },
  ],
};

export default {
  name: "TopUser",
  components: {
    NavTabs,
    RestaurantsUserTop,
  },

  data() {
    return {
      users: [],
    };
  },

  created() {
    this.fetchUsersTop();
  },

  methods: {
    fetchUsersTop() {
      const { users } = dummyUsers;
      this.users = users;
    },
  },
};
</script>