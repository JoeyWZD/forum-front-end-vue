<template>
  <div class="container py-5">
    <div>
      <h1>{{ restaurant.name }}</h1>
      <span class="badge badge-secondary mt-1 mb-3">
        {{ restaurant.categoryName ? restaurant.categoryName : "未分類" }}
      </span>
    </div>

    <hr />

    <ul>
      <li>
        評論數：
        {{ restaurant.commentsLength ? restaurant.commentsLength : "0" }}
      </li>
      <li>瀏覽次數： {{ restaurant.viewCounts }}</li>
    </ul>

    <button type="button" class="btn btn-link" @click="$router.back()">
      回上一頁
    </button>
  </div>
</template>

<script>
import restaurantsAPI from "./../apis/restaurants";
import { Toast } from "./../utils/helpers";

export default {
  data() {
    return {
      restaurant: {
        id: -1,
        name: "",
        viewCounts: 0,
        Category: {},
        Comments: [],
      },
    };
  },

  created() {
    const { id: restaurantId } = this.$route.params;
    this.fetchData(restaurantId);
  },
  // 手動更改網址時要跳轉
  beforeRouteUpdate(to, from, next) {
    const { id: restaurantId } = to.params;
    this.fetchRestaurantDashboard(restaurantId);
    next();
  },

  methods: {
    async fetchData(restaurantId) {
      try {
        const { data } = await restaurantsAPI.getRestaurant({ restaurantId });
        console.log(data);
        const { id, name, viewCounts, Category, Comments } = data.restaurant;
        this.restaurant = {
          ...this.restaurant,
          id,
          name,
          categoryName: Category ? Category.name : "未分類",
          commentsLength: Comments.length,
          viewCounts,
        };
      } catch (error) {
        Toast.fire({
          icon: "error",
          title: "無法取得餐廳資料，請稍後再試",
        });
      }
    },
  },
};
</script>