<template>
  <div class="container py-5">
    <NavTabs />
    <!-- 餐廳類別標籤 RestaurantsNavPills -->
    <RestaurantsNavPills
      :categories="categories"
    />

    <div class="row">
      <!-- 餐廳卡片 RestaurantCard-->
      <RestaurantCard
        v-for="restaurant in restaurants"
        :key="restaurant.id"
        :initial-restaurant="restaurant"
      />
    </div>

    <!-- 分頁標籤 RestaurantPagination -->
     <RestaurantsPagination
      v-if="totalPage.length > 1"
      :current-page="currentPage"
      :total-page="totalPage"
      :category-id="categoryId"
      :previous-page="previousPage"
      :next-page="nextPage"
    />
  </div>
</template>

<script>
import NavTabs from "./../components/NavTabs";
import RestaurantCard from "./../components/RestaurantCard.vue";
import RestaurantsNavPills from "./../components/RestaurantsNavPills.vue";
import RestaurantsPagination from "./../components/RestaurantsPagination.vue";

const dummyData = {
  restaurants: [
    {
      id: 1,
      name: "Monroe Rohan",
      tel: "1-046-579-1686 x62187",
      address: "028 Funk Summit",
      opening_hours: "08:00",
      description: "Est aut officia incidunt doloribus voluptas sed qu",
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
      isFavorited: false,
      isLiked: false,
    },
    {
      id: 2,
      name: "April Wolf",
      tel: "037.052.8238",
      address: "92829 Shannon Roads",
      opening_hours: "08:00",
      description: "Nihil doloremque voluptatem unde quis quia libero ",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=59.95278885959543",
      viewCounts: 0,
      createdAt: "2022-07-08T05:38:02.000Z",
      updatedAt: "2022-07-08T05:38:02.000Z",
      CategoryId: 4,
      Category: {
        id: 4,
        name: "墨西哥料理",
        createdAt: "2022-07-08T05:38:02.000Z",
        updatedAt: "2022-07-08T05:38:02.000Z",
      },
      isFavorited: false,
      isLiked: false,
    },
    {
      id: 3,
      name: "Skyla Ebert",
      tel: "340-901-0863 x99286",
      address: "0410 Hickle Flats",
      opening_hours: "08:00",
      description: "Delectus corrupti voluptates nisi incidunt volupta",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=10.852470285042282",
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
      isFavorited: false,
      isLiked: false,
    },
    {
      id: 4,
      name: "Newton Eichmann",
      tel: "1-512-578-0055",
      address: "265 O'Kon Road",
      opening_hours: "08:00",
      description: "saepe non neque",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=11.756119959581834",
      viewCounts: 0,
      createdAt: "2022-07-08T05:38:02.000Z",
      updatedAt: "2022-07-08T05:38:02.000Z",
      CategoryId: 4,
      Category: {
        id: 4,
        name: "墨西哥料理",
        createdAt: "2022-07-08T05:38:02.000Z",
        updatedAt: "2022-07-08T05:38:02.000Z",
      },
      isFavorited: false,
      isLiked: false,
    },
    {
      id: 5,
      name: "Immanuel Blanda",
      tel: "235-106-5879 x23171",
      address: "74576 Layne Meadows",
      opening_hours: "08:00",
      description: "Ex harum sequi cum inventore libero ut ducimus deb",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=13.882071847365873",
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
      isFavorited: false,
      isLiked: false,
    },
    {
      id: 6,
      name: "Cicero Torp",
      tel: "(709) 158-0170",
      address: "78878 Will Hills",
      opening_hours: "08:00",
      description: "saepe",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=67.82181637207141",
      viewCounts: 0,
      createdAt: "2022-07-08T05:38:02.000Z",
      updatedAt: "2022-07-08T05:38:02.000Z",
      CategoryId: 1,
      Category: {
        id: 1,
        name: "中式料理",
        createdAt: "2022-07-08T05:38:02.000Z",
        updatedAt: "2022-07-08T05:38:02.000Z",
      },
      isFavorited: false,
      isLiked: false,
    },
    {
      id: 7,
      name: "Tom Metz",
      tel: "1-918-560-6900",
      address: "60313 Preston Square",
      opening_hours: "08:00",
      description: "Dolor modi velit. Qui deleniti fugiat. Architecto ",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=30.446407878959448",
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
      isFavorited: false,
      isLiked: false,
    },
    {
      id: 8,
      name: "Lenny Cronin",
      tel: "(088) 008-9435",
      address: "409 Erika Lock",
      opening_hours: "08:00",
      description: "Amet adipisci provident repudiandae tenetur ad.\nOp",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=24.72036498654102",
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
      isFavorited: false,
      isLiked: false,
    },
    {
      id: 9,
      name: "Taya Glover IV",
      tel: "336.149.6111 x812",
      address: "52245 Sammy Well",
      opening_hours: "08:00",
      description: "Incidunt explicabo alias.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=51.11780678683591",
      viewCounts: 0,
      createdAt: "2022-07-08T05:38:02.000Z",
      updatedAt: "2022-07-08T05:38:02.000Z",
      CategoryId: 1,
      Category: {
        id: 1,
        name: "中式料理",
        createdAt: "2022-07-08T05:38:02.000Z",
        updatedAt: "2022-07-08T05:38:02.000Z",
      },
      isFavorited: false,
      isLiked: false,
    },
    {
      id: 10,
      name: "Mabel Schumm",
      tel: "(833) 048-5571 x02264",
      address: "002 Keeling Harbor",
      opening_hours: "08:00",
      description: "Laudantium magni voluptatibus voluptatibus rerum. ",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=68.15129519913454",
      viewCounts: 0,
      createdAt: "2022-07-08T05:38:02.000Z",
      updatedAt: "2022-07-08T05:38:02.000Z",
      CategoryId: 4,
      Category: {
        id: 4,
        name: "墨西哥料理",
        createdAt: "2022-07-08T05:38:02.000Z",
        updatedAt: "2022-07-08T05:38:02.000Z",
      },
      isFavorited: false,
      isLiked: false,
    },
  ],
  categories: [
    {
      id: 1,
      name: "中式料理",
      createdAt: "2022-07-08T05:38:02.000Z",
      updatedAt: "2022-07-08T05:38:02.000Z",
    },
    {
      id: 2,
      name: "日本料理",
      createdAt: "2022-07-08T05:38:02.000Z",
      updatedAt: "2022-07-08T05:38:02.000Z",
    },
    {
      id: 3,
      name: "義大利料理",
      createdAt: "2022-07-08T05:38:02.000Z",
      updatedAt: "2022-07-08T05:38:02.000Z",
    },
    {
      id: 4,
      name: "墨西哥料理",
      createdAt: "2022-07-08T05:38:02.000Z",
      updatedAt: "2022-07-08T05:38:02.000Z",
    },
    {
      id: 5,
      name: "素食料理",
      createdAt: "2022-07-08T05:38:02.000Z",
      updatedAt: "2022-07-08T05:38:02.000Z",
    },
    {
      id: 6,
      name: "美式料理",
      createdAt: "2022-07-08T05:38:02.000Z",
      updatedAt: "2022-07-08T05:38:02.000Z",
    },
    {
      id: 7,
      name: "複合式料理",
      createdAt: "2022-07-08T05:38:02.000Z",
      updatedAt: "2022-07-08T05:38:02.000Z",
    },
  ],
  categoryId: "",
  page: 1,
  totalPage: [1, 2, 3, 4, 5],
  prev: 1,
  next: 2,
};

export default {
  components: {
    NavTabs,
    RestaurantCard,
    RestaurantsNavPills,
    RestaurantsPagination
  },

  data() {
    return {
      restaurants: [],
      categories: [],
      categoryId: -1,
      currentPage: 1,
      totalPage: [],
      previousPage: -1,
      nextPage: -1,
    };
  },

  created() {
    this.fetchRestaurants();
  },

  methods: {
    fetchRestaurants() {
      const {
        restaurants,
        categories,
        categoryId,
        page,
        totalPage,
        prev,
        next,
      } = dummyData;
      this.restaurants = restaurants;
      this.categories = categories;
      this.categoryId = categoryId;
      this.currentPage = page;
      this.totalPage = totalPage;
      this.previousPage = prev;
      this.nextPage = next;
    },
  },
};
</script>