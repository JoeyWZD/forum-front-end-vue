<template>
  <div class="card">
    <div class="card-header">
      <strong>{{ favoriteRestaurant.length }}</strong> 收藏的餐廳
    </div>
    <div class="card-body">
      <router-link
        :to="{ name: 'restaurant', params: { id: restaurant.id } }"
        v-for="restaurant in favoriteRestaurant"
        :key="restaurant.id"
      >
        <img :src="restaurant.image" class="avatar" width="60" height="60" />
      </router-link>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    userFavoritedRestaurants: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      favoriteRestaurant: this.userFavoritedRestaurants,
    };
  },
};
</script>