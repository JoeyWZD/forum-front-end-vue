<template>
  <div class="container py-5">
    <NavTabs />
    <h1 class="mt-5">人氣餐廳</h1>

    <hr />
    <div
      class="card mb-3"
      style="max-width: 540px; margin: auto"
      v-for="restaurant in restaurants"
      :key="restaurant.id"
    >
      <div class="row no-gutters">
        <div class="col-md-4">
          <router-link :to="{name: 'restaurant', params: {id: restaurant.id } }">
            <img class="card-img" :src="restaurant.image" />
          </router-link>
        </div>
        <div class="col-md-8">
          <div class="card-body">
            <h5 class="card-title">{{ restaurant.name }}</h5>
            <span class="badge badge-secondary">{{restaurant.FavoriteCount}}</span>
            <p class="card-text">
              {{ restaurant.description }}
            </p>
            <a href="#" class="btn btn-primary mr-2">Show</a>

            <button
              type="button"
              class="btn btn-danger mr-2"
              v-if="restaurant.isFavorited"
              @click.stop.prevent="deleteFavorite(restaurant.id)"
            >
              移除最愛
            </button>
            <button
              type="button"
              class="btn btn-primary"
              v-else
              @click.stop.prevent="addFavorite(restaurant.id)"
            >
              加到最愛
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import NavTabs from "./../components/NavTabs";

const dummyData = {
  restaurants: [
    {
      id: 50,
      name: "Elza Rolfson",
      tel: "380-904-3024 x067",
      address: "980 Bruen Squares",
      opening_hours: "08:00",
      description: "Ratione labore est accusantium saepe est repellend",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=32.902975919022445",
      viewCounts: 0,
      createdAt: "2022-07-08T05:38:02.000Z",
      updatedAt: "2022-07-08T05:38:02.000Z",
      CategoryId: 4,
      FavoritedUsers: [],
      isFavorited: false,
      FavoriteCount: 0,
    },
    {
      id: 49,
      name: "Trace Barton",
      tel: "1-970-228-3927 x87273",
      address: "451 Gerlach Mountains",
      opening_hours: "08:00",
      description: "Aut ad at reprehenderit iure cum corrupti optio vo",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=1.6287841142439197",
      viewCounts: 0,
      createdAt: "2022-07-08T05:38:02.000Z",
      updatedAt: "2022-07-08T05:38:02.000Z",
      CategoryId: 5,
      FavoritedUsers: [],
      isFavorited: false,
      FavoriteCount: 0,
    },
    {
      id: 48,
      name: "Willis Hegmann",
      tel: "1-296-791-7152 x2101",
      address: "438 Berge Ridges",
      opening_hours: "08:00",
      description: "Pariatur suscipit vel non ipsam mollitia numquam.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=92.14719814879288",
      viewCounts: 0,
      createdAt: "2022-07-08T05:38:02.000Z",
      updatedAt: "2022-07-08T05:38:02.000Z",
      CategoryId: 4,
      FavoritedUsers: [],
      isFavorited: false,
      FavoriteCount: 0,
    },
    {
      id: 47,
      name: "Harmon Kuhn PhD",
      tel: "342-389-7219 x899",
      address: "67602 Gutkowski Tunnel",
      opening_hours: "08:00",
      description: "Similique aperiam qui dicta et consectetur volupta",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=43.20310477250855",
      viewCounts: 0,
      createdAt: "2022-07-08T05:38:02.000Z",
      updatedAt: "2022-07-08T05:38:02.000Z",
      CategoryId: 4,
      FavoritedUsers: [],
      isFavorited: false,
      FavoriteCount: 0,
    },
    {
      id: 46,
      name: "Mr. Aliyah Gibson",
      tel: "314-739-8142",
      address: "557 Vivien Ville",
      opening_hours: "08:00",
      description: "eos molestias numquam",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=29.157333455913626",
      viewCounts: 0,
      createdAt: "2022-07-08T05:38:02.000Z",
      updatedAt: "2022-07-08T05:38:02.000Z",
      CategoryId: 2,
      FavoritedUsers: [],
      isFavorited: false,
      FavoriteCount: 0,
    },
    {
      id: 45,
      name: "Lesley Reilly",
      tel: "358.905.7411",
      address: "4789 Purdy Square",
      opening_hours: "08:00",
      description: "Impedit aliquam perspiciatis. Sed molestias quibus",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=68.09118344813258",
      viewCounts: 0,
      createdAt: "2022-07-08T05:38:02.000Z",
      updatedAt: "2022-07-08T05:38:02.000Z",
      CategoryId: 3,
      FavoritedUsers: [],
      isFavorited: false,
      FavoriteCount: 0,
    },
    {
      id: 44,
      name: "Alek Dooley",
      tel: "824.020.9809",
      address: "96020 Sawayn Keys",
      opening_hours: "08:00",
      description: "Modi quis voluptatem et labore dolorum ullam. Cons",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=10.032549212094644",
      viewCounts: 0,
      createdAt: "2022-07-08T05:38:02.000Z",
      updatedAt: "2022-07-08T05:38:02.000Z",
      CategoryId: 4,
      FavoritedUsers: [],
      isFavorited: false,
      FavoriteCount: 0,
    },
    {
      id: 43,
      name: "Audreanne Ward",
      tel: "965-658-8223 x3855",
      address: "61015 Dietrich Circles",
      opening_hours: "08:00",
      description: "Id non quas optio qui a. Rerum facilis perferendis",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=98.12452595686247",
      viewCounts: 0,
      createdAt: "2022-07-08T05:38:02.000Z",
      updatedAt: "2022-07-08T05:38:02.000Z",
      CategoryId: 5,
      FavoritedUsers: [],
      isFavorited: false,
      FavoriteCount: 0,
    },
    {
      id: 42,
      name: "Elenora Runolfsson",
      tel: "269-550-1482 x854",
      address: "98315 Nikolaus Crest",
      opening_hours: "08:00",
      description: "Repellat eius aut voluptates inventore illo animi ",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=76.32462170543035",
      viewCounts: 0,
      createdAt: "2022-07-08T05:38:02.000Z",
      updatedAt: "2022-07-08T05:38:02.000Z",
      CategoryId: 5,
      FavoritedUsers: [],
      isFavorited: false,
      FavoriteCount: 0,
    },
    {
      id: 41,
      name: "Marilou Hilpert",
      tel: "(845) 176-6057",
      address: "165 Marquardt Plain",
      opening_hours: "08:00",
      description: "iure minima quod",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=62.216210043953566",
      viewCounts: 0,
      createdAt: "2022-07-08T05:38:02.000Z",
      updatedAt: "2022-07-08T05:38:02.000Z",
      CategoryId: 1,
      FavoritedUsers: [],
      isFavorited: false,
      FavoriteCount: 0,
    },
  ],
};

export default {
  components: {
    NavTabs,
  },

  data() {
    return {
      restaurants: [],
    };
  },

  created() {
    this.fetchaTops();
  },

  methods: {
    fetchaTops() {
      this.restaurants = dummyData.restaurants;
    },
    //不使用component 的話，就要重新上傳新的陣列(修改)
    addFavorite(restaurantId) {
      this.restaurants = this.restaurants.map((restaurant) => {
        return restaurant.id === restaurantId
          ? {
              ...restaurant,
              FavoriteCount: restaurant.FavoriteCount + 1,
              isFavorited: true,
            }
          : restaurant;
      });
    },

    deleteFavorite(restaurantId) {
      this.restaurants = this.restaurants.map((restaurant) => {
        return restaurant.id === restaurantId
          ? {
              ...restaurant,
              FavoriteCount: restaurant.FavoriteCount - 1,
              isFavorited: false,
            }
          : restaurant;
      });
    },
  },
};
</script>