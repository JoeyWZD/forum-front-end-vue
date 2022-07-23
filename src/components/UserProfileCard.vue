<template>
  <div class="card mb-3">
    <div class="row no-gutters">
      <div class="col-md-4">
        <img :src="userProfile.image" width="300px" height="300px" />
      </div>
      <div class="col-md-8">
        <div class="card-body">
          <h5 class="card-title">{{ userProfile.name }}</h5>
          <p class="card-text">{{ userProfile.email }}</p>
          <ul class="list-unstyled list-inline">
            <li>
              <strong>{{ userProfile.Comments.length }}</strong> 已評論餐廳
            </li>
            <li>
              <strong>{{ userProfile.FavoritedRestaurants.length }}</strong>
              收藏的餐廳
            </li>
            <li>
              <strong>{{ userProfile.Followers.length }}</strong> followings
              (追蹤者)
            </li>
            <li>
              <strong>{{ userProfile.Followings.length }}</strong> followers
              (追隨者)
            </li>
          </ul>
          <p></p>
          <form
            action="/following/1?_method=DELETE"
            method="POST"
            style="display: contents"
          >
            <template v-if="isCurrentUser">
              <router-link
                :to="{ name: 'user-edit', params: { id: userProfile.id } }"
                class="btn btn-primary"
              >
                Edit
              </router-link></template
            >
            <template v-else>
              <button
                v-if="isFollowed"
                @click.prevent.stop="cancelFollow(user.id)"
                type="submit"
                class="btn btn-danger"
              >
                取消追蹤
              </button>
              <button
                v-else
                type="submit"
                @click.prevent.stop="addFollow(user.id)"
                class="btn btn-primary"
              >
                追蹤
              </button>
            </template>
          </form>
          <p></p>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import usersAPI from "./../apis/users.js";
import { Toast } from "./../utils/helpers";

export default {
  props: {
    user: {
      required: true,
      type: Object,
    },
    isCurrentUser: {
      type: Boolean,
      required: true,
    },
    initialIsFollowed: {
      required: true,
      type: Boolean,
    },
  },
  data() {
    return {
      userProfile: this.user,
      isFollowed: this.initialIsFollowed,
    };
  },

  watch: {
    // 父元件非同步渲染，會最後才將資料傳遞子元件
    initialIsFollowed(newVal) {
      this.isFollowed = newVal;
    },
  },
  methods: {
    async addFollow(userId) {
      try {
        const { data } = await usersAPI.addFollowing({ userId });
        if (data.status !== "success") {
          throw new Error(data.message);
        }

        this.isFollowed = true;
      } catch (error) {
        Toast.fire({
          icon: "error",
          title: "無法追蹤，請稍後再試",
        });
      }
    },
    async cancelFollow(userId) {
      try {
        const { data } = await usersAPI.deleteFollowing({ userId });
        if (data.status !== "success") {
          throw new Error(data.message);
        }

        this.isFollowed = false;
      } catch (error) {
        Toast.fire({
          icon: "error",
          title: "無法取消追蹤，請稍後再試",
        });
      }
    },
  },
};
</script>