<template>
  <div>
    <div class="col-3">
      <router-link :to="{ name: 'user-profile', params: { id: user.id } }">
        <img :src="user.image" width="140px" height="140px" />
      </router-link>
      <h2>{{ user.name }}</h2>
      <span class="badge badge-secondary"
        >追蹤人數：{{ user.FollowerCount }}</span
      >
      <p class="mt-3">
        <button
          type="button"
          class="btn btn-primary"
          v-if="!user.isFollowed"
          @click.stop.prevent="addFollow"
        >
          追蹤
        </button>

        <button
          type="button"
          class="btn btn-danger"
          v-else
          @click.stop.prevent="removeFollow"
        >
          取消追蹤
        </button>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    initialUser: {
      type: Object,
      required: true,
    },
  },

  data() {
    return {
      user: this.initialUser,
    };
  },

  methods: {
    addFollow() {
      this.user = {
        ...this.user, // 保留餐廳內原有資料
        isFollowed: true,
      };
    },

    removeFollow() {
      this.user = {
        ...this.user, // 保留餐廳內原有資料
        isFollowed: false,
      };
    },
  },
};
</script>