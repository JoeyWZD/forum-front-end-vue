<template>
  <div class="container py-5">
    <!-- 餐廳資訊頁 RestaurantDetail -->
    <RestaurantDetail :initial-restaurant="restaurant" />

    <hr />
    <!-- 餐廳評論 RestaurantComments -->
    <RestaurantComments
      :restaurant-comments="restaurantComments"
      @after-delete-comment="afterDeleteComment"
    />
    <!-- 新增評論 CreateComment -->
    <CreateComment
      :restaurant-id="restaurant.id"
      @after-create-comment="afterCreateComment"
    />
  </div>
</template>

<script>
import RestaurantDetail from "./../components/RestaurantDetail.vue";
import RestaurantComments from "./../components/RestaurantComments.vue";
import CreateComment from "./../components/CreateComment.vue";

const dummyData = {
  restaurant: {
    id: 1,
    name: "Franco Boyer",
    tel: "(765) 610-2179 x21150",
    address: "65008 Eusebio Summit",
    opening_hours: "08:00",
    description: "sapiente ex nihil",
    image:
      "https://loremflickr.com/320/240/restaurant,food/?random=65.02882729727115",
    viewCounts: 1,
    createdAt: "2022-07-02T19:36:40.000Z",
    updatedAt: "2022-07-05T20:47:25.275Z",
    CategoryId: 4,
    Category: {
      id: 4,
      name: "墨西哥料理",
      createdAt: "2022-07-02T19:36:40.000Z",
      updatedAt: "2022-07-02T19:36:40.000Z",
    },
    FavoritedUsers: [],
    LikedUsers: [],
    Comments: [
      {
        id: 1,
        text: "Voluptates enim nisi ad enim perspiciatis possimus.",
        UserId: 1,
        RestaurantId: 1,
        createdAt: "2022-07-02T19:36:40.000Z",
        updatedAt: "2022-07-02T19:36:40.000Z",
        User: {
          id: 1,
          name: "root",
          email: "root@example.com",
          password:
            "$2a$10$75ECfZeCAP6jjrtfRQY6M.JmmqFFkOSlFoN41j7w1VjmYcWNlh7PW",
          isAdmin: true,
          image: null,
          createdAt: "2022-07-02T19:36:40.000Z",
          updatedAt: "2022-07-02T19:36:40.000Z",
        },
      },
      {
        id: 51,
        text: "Porro et illo vel voluptas et soluta voluptate blanditiis.",
        UserId: 1,
        RestaurantId: 1,
        createdAt: "2022-07-02T19:36:40.000Z",
        updatedAt: "2022-07-02T19:36:40.000Z",
        User: {
          id: 1,
          name: "root",
          email: "root@example.com",
          password:
            "$2a$10$75ECfZeCAP6jjrtfRQY6M.JmmqFFkOSlFoN41j7w1VjmYcWNlh7PW",
          isAdmin: true,
          image: null,
          createdAt: "2022-07-02T19:36:40.000Z",
          updatedAt: "2022-07-02T19:36:40.000Z",
        },
      },
      {
        id: 101,
        text: "Quos consectetur optio hic labore.",
        UserId: 1,
        RestaurantId: 1,
        createdAt: "2022-07-02T19:36:40.000Z",
        updatedAt: "2022-07-02T19:36:40.000Z",
        User: {
          id: 1,
          name: "root",
          email: "root@example.com",
          password:
            "$2a$10$75ECfZeCAP6jjrtfRQY6M.JmmqFFkOSlFoN41j7w1VjmYcWNlh7PW",
          isAdmin: true,
          image: null,
          createdAt: "2022-07-02T19:36:40.000Z",
          updatedAt: "2022-07-02T19:36:40.000Z",
        },
      },
    ],
  },
  isFavorited: false,
  isLiked: false,
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

export default {
  components: {
    RestaurantDetail,
    RestaurantComments,
    CreateComment,
  },

  data() {
    return {
      restaurant: {
        id: -1,
        name: "",
        categoryName: "",
        image: "",
        openingHours: "",
        tel: "",
        address: "",
        description: "",
        isFavorited: false,
        isLiked: false,
      },
      currentUser: dummyUser.currentUser,
      restaurantComments: [],
    };
  },
  created() {
    const { id: restaurantId } = this.$route.params;
    this.fetchRestaurant(restaurantId);
  },
  methods: {
    fetchRestaurant(restaurantId) {
      console.log("fetchRestaurant id: ", restaurantId);

      this.restaurant = {
        id: dummyData.restaurant.id,
        name: dummyData.restaurant.name,
        categoryName: dummyData.restaurant.Category.name,
        image: dummyData.restaurant.image,
        openingHours: dummyData.restaurant.opening_hours,
        tel: dummyData.restaurant.tel,
        address: dummyData.restaurant.address,
        description: dummyData.restaurant.description,
        isFavorited: dummyData.isFavorited,
        isLiked: dummyData.isLiked,
      };

      this.restaurantComments = dummyData.restaurant.Comments;
    },
    afterDeleteComment(commentId) {
      // 以 filter 保留未被選擇的 comment.id
      this.restaurantComments = this.restaurantComments.filter(
        (comment) => comment.id !== commentId
      );
    },

    afterCreateComment(payload) {
      const { commentId, restaurantId, text } = payload;
      this.restaurantComments.push({
        id: commentId,
        RestaurantId: restaurantId,
        User: {
          id: this.currentUser.id,
          name: this.currentUser.name,
        },
        text,
        createdAt: new Date(),
      });
    },
  },
};
</script>