<template>
  <div class="album py-5 bg-light">
    <div class="container">
      <!-- UserProfileCard -->
      <UserProfileCard
        :user="user"
        :initial-is-followed="isFollowed"
        :is-current-user="currentUser.id === user.id"
      />
      <div class="row">
        <div class="col-md-4">
          <UserFollowingsCard :user-followings="user.Followings" />
          <br />
          <UserFollowersCard :user-followers="user.Followers" />
        </div>
        <div class="col-md-8">
          <UserCommentsCard :user-comment="user.Comments" />
          <br />
          <UserFavoritedRestaurantsCard
            :user-favorited-restaurants="user.FavoritedRestaurants"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import UserProfileCard from "./../components/UserProfileCard.vue";
import UserFollowingsCard from "./../components/UserFollowingsCard.vue";
import UserFollowersCard from "./../components/UserFollowersCard.vue";
import UserCommentsCard from "./../components/UserCommentsCard.vue";
import UserFavoritedRestaurantsCard from "./../components/UserFavoritedRestaurantsCard.vue";
import usersAPI from "./../apis/users.js";
import { Toast } from "./../utils/helpers";
import { mapState } from "vuex";

export default {
  components: {
    UserProfileCard,
    UserFollowingsCard,
    UserFollowersCard,
    UserCommentsCard,
    UserFavoritedRestaurantsCard,
  },

  data() {
    return {
      user: {
        id: -1,
        name: "",
        email: "",
        image: "",
        Comments: [],
        FavoritedRestaurants: [],
        Followers: [],
        Followings: [],
      },
      isFollowed: false,
    };
  },
  created() {
    const { id } = this.$route.params;
    this.fetchUser(id);
  },
  computed: {
    ...mapState(["currentUser"]),
  },
  beforeRouteUpdate(to, from, next) {
    const { id } = to.params;
    this.fetchUser(id);
    next();
  },
  methods: {
    async fetchUser(userId) {
      try {
        const { data } = await usersAPI.get({ userId });
        const { profile, isFollowed } = data;
        console.log(isFollowed);
        const {
          id,
          name,
          email,
          image,
          Comments,
          FavoritedRestaurants,
          Followers,
          Followings,
        } = profile;
        this.user = {
          id,
          name,
          email,
          image,
          Comments,
          FavoritedRestaurants,
          Followers,
          Followings,
        };
        this.isFollowed = isFollowed;
      } catch (error) {
        Toast.fire({
          icon: "error",
          title: "無法取得使用者資料，請稍後再試",
        });
      }
    },
  },
};
</script>