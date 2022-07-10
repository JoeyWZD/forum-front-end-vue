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
const dummyData = {
  restaurant: {
    id: 1,
    name: "Monroe Rohan",
    tel: "1-046-579-1686 x62187",
    address: "028 Funk Summit",
    opening_hours: "08:00",
    description:
      "Est aut officia incidunt doloribus voluptas sed quia ad debitis. Saepe odio molestias blanditiis laudantium.",
    image:
      "https://loremflickr.com/320/240/restaurant,food/?random=23.5657968347033",
    viewCounts: 0,
    createdAt: "2022-07-08T05:38:02.000Z",
    updatedAt: "2022-07-08T05:38:02.000Z",
    CategoryId: 5,
    Category: {
      id: 5,
      name: "素食料理",
      createdAt: "2022-07-08T05:38:02.000Z",
      updatedAt: "2022-07-08T05:38:02.000Z",
    },
    Comments: [
      {
        id: 1,
        text: "Natus neque nihil est necessitatibus.",
        UserId: 1,
        RestaurantId: 1,
        createdAt: "2022-07-08T05:38:02.000Z",
        updatedAt: "2022-07-08T05:38:02.000Z",
        User: {
          id: 1,
          name: "root",
          email: "root@example.com",
          password:
            "$2a$10$10JUqZOmUsK0LblbEJHaJ.EYvrjkj0ytEPrwvPF4FfDIUjxlBtIZO",
          isAdmin: true,
          image: null,
          createdAt: "2022-07-08T05:38:02.000Z",
          updatedAt: "2022-07-08T05:38:02.000Z",
        },
      },
      {
        id: 101,
        text: "Sit cupiditate aliquam ut praesentium at eaque veritatis ea dolores.",
        UserId: 2,
        RestaurantId: 1,
        createdAt: "2022-07-08T05:38:02.000Z",
        updatedAt: "2022-07-08T05:38:02.000Z",
        User: {
          id: 2,
          name: "user1",
          email: "user1@example.com",
          password:
            "$2a$10$SfMkNk.RcqJws7HRD5xl/umoL59oLIVSSv8jfDvCfckLrV05ZdEnO",
          isAdmin: false,
          image: null,
          createdAt: "2022-07-08T05:38:02.000Z",
          updatedAt: "2022-07-08T05:38:02.000Z",
        },
      },
      {
        id: 51,
        text: "Dolor debitis aut asperiores voluptas nisi voluptatem veritatis.",
        UserId: 3,
        RestaurantId: 1,
        createdAt: "2022-07-08T05:38:02.000Z",
        updatedAt: "2022-07-08T05:38:02.000Z",
        User: {
          id: 3,
          name: "user2",
          email: "user2@example.com",
          password:
            "$2a$10$RIzFHpfPqTjgjUbQDGFksu2ebkPC5QW40GTiwXt6vnFWbNbnCR7OO",
          isAdmin: false,
          image: null,
          createdAt: "2022-07-08T05:38:02.000Z",
          updatedAt: "2022-07-08T05:38:02.000Z",
        },
      },
    ],
  },
};

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
    this.fetchData();
  },

  methods: {
    fetchData() {
      const { id, name, viewCounts, Category, Comments } = dummyData.restaurant;
      this.restaurant = {
        ...this.restaurant,
        id,
        name,
        categoryName: Category ? Category.name : "未分類",
        commentsLength: Comments.length,
        viewCounts,
      };
    },
  },
};
</script>