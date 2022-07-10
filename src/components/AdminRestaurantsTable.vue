<template>
  <table class="table">
    <thead class="thead-dark">
      <tr>
        <th scope="col">#</th>
        <th scope="col">Category</th>
        <th scope="col">Name</th>
        <th scope="col" width="300">操作</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="restaurant in restaurants" :key="restaurant.id">
        <th scope="row">
          {{ restaurant.id }}
        </th>
        <td>{{ restaurant.Category ? restaurant.Category.name : "未分類" }}</td>
        <td>{{ restaurant.name }}</td>
        <td class="d-flex justify-content-between">
          <router-link
            :to="{ name: 'admin-restaurant', params: { id: restaurant.id } }"
            class="btn btn-link"
            >Show</router-link
          >

          <router-link :to="{name : 'admin-restaurant-edit', params: {id : restaurant.id} }" class="btn btn-link">Edit</router-link>

          <button
            type="button"
            class="btn btn-link"
            @click.stop.prevent="deleteRestaurant(restaurant.id)"
          >
            Delete
          </button>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
const dummyData =
  // ... 請貼上 API 資料
  {
    restaurants: [
      {
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
      },
      {
        id: 2,
        name: "April Wolf",
        tel: "037.052.8238",
        address: "92829 Shannon Roads",
        opening_hours: "08:00",
        description:
          "Nihil doloremque voluptatem unde quis quia libero repellendus.\nDolor veritatis ducimus omnis nemo maxime facilis qui enim.",
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
      },
      {
        id: 3,
        name: "Skyla Ebert",
        tel: "340-901-0863 x99286",
        address: "0410 Hickle Flats",
        opening_hours: "08:00",
        description:
          "Delectus corrupti voluptates nisi incidunt voluptatum cum aut aut veniam. Itaque neque repudiandae quo veritatis. Et facere eligendi saepe non. Atque velit necessitatibus voluptas error harum.\n \rDicta ad quas optio adipisci. Ut dolorem occaecati. Ab id vero facere. Ullam voluptas voluptatem est voluptatem possimus iusto adipisci fugiat.\n \rRerum nihil reiciendis et fugiat repellat dolorum deserunt. Enim at dolores sunt esse. Et maiores nihil voluptate suscipit enim. Rem quia officiis. Dolores consequatur corrupti eius.",
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
      },
      {
        id: 5,
        name: "Immanuel Blanda",
        tel: "235-106-5879 x23171",
        address: "74576 Layne Meadows",
        opening_hours: "08:00",
        description:
          "Ex harum sequi cum inventore libero ut ducimus debitis omnis. Qui enim placeat minima quas eos eos eos nihil ad. Sequi omnis laborum magni.",
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
      },
      {
        id: 7,
        name: "Tom Metz",
        tel: "1-918-560-6900",
        address: "60313 Preston Square",
        opening_hours: "08:00",
        description:
          "Dolor modi velit. Qui deleniti fugiat. Architecto commodi ut culpa beatae.",
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
      },
      {
        id: 8,
        name: "Lenny Cronin",
        tel: "(088) 008-9435",
        address: "409 Erika Lock",
        opening_hours: "08:00",
        description:
          "Amet adipisci provident repudiandae tenetur ad.\nOptio quis minus autem.",
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
      },
      {
        id: 10,
        name: "Mabel Schumm",
        tel: "(833) 048-5571 x02264",
        address: "002 Keeling Harbor",
        opening_hours: "08:00",
        description:
          "Laudantium magni voluptatibus voluptatibus rerum. Ratione culpa unde voluptas facilis eos. Molestiae id officiis tempora tempora id magnam et temporibus repellendus. Dignissimos et ratione quia et.\n \rBlanditiis doloribus omnis blanditiis. Quisquam est laboriosam accusantium quia. Maxime omnis aut omnis perferendis aut fugiat. Omnis nihil dolorum tenetur sit ipsa voluptatem sed. Impedit earum consequuntur consequatur. Ratione dolorum impedit earum sed in aliquam ipsa.\n \rItaque aliquam totam dolor. Similique illo nostrum aut itaque vel sit dolorum. Dignissimos natus molestias et veniam. Quo quia explicabo sunt. Et amet non. Et enim ut sed suscipit et ipsa sit vitae officiis.",
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
      },
      {
        id: 11,
        name: "Abner Rice",
        tel: "490-750-7378 x29115",
        address: "202 Lilian Valley",
        opening_hours: "08:00",
        description:
          "Iusto et consequatur aut temporibus ut quia tempora molestiae.",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=71.09772797347573",
        viewCounts: 0,
        createdAt: "2022-07-08T05:38:02.000Z",
        updatedAt: "2022-07-08T05:38:02.000Z",
        CategoryId: 3,
        Category: {
          id: 3,
          name: "義大利料理",
          createdAt: "2022-07-08T05:38:02.000Z",
          updatedAt: "2022-07-08T05:38:02.000Z",
        },
      },
      {
        id: 12,
        name: "Mr. Deshawn Wyman",
        tel: "296.305.9251",
        address: "0827 Koepp Oval",
        opening_hours: "08:00",
        description: "tempore",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=73.13315171463294",
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
      },
      {
        id: 13,
        name: "Dr. Ladarius Stoltenberg",
        tel: "(518) 418-2135",
        address: "7057 Ardella Burg",
        opening_hours: "08:00",
        description:
          "Dolorem beatae enim architecto cumque eligendi adipisci nulla.\nExercitationem doloremque voluptatum occaecati repudiandae rerum.",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=48.25125283298579",
        viewCounts: 0,
        createdAt: "2022-07-08T05:38:02.000Z",
        updatedAt: "2022-07-08T05:38:02.000Z",
        CategoryId: 2,
        Category: {
          id: 2,
          name: "日本料理",
          createdAt: "2022-07-08T05:38:02.000Z",
          updatedAt: "2022-07-08T05:38:02.000Z",
        },
      },
      {
        id: 14,
        name: "Ardith McLaughlin",
        tel: "(905) 112-3791",
        address: "790 Williamson Lodge",
        opening_hours: "08:00",
        description: "veritatis",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=58.182797732376535",
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
      },
      {
        id: 15,
        name: "Ryleigh Brekke",
        tel: "113.280.2500",
        address: "607 America Brooks",
        opening_hours: "08:00",
        description:
          "A voluptatem eum. Nostrum qui sunt aut dolorem. Et alias cupiditate non similique. Voluptas deleniti delectus sit blanditiis at cupiditate in aspernatur. Sunt voluptatem iste debitis impedit error dolorem.",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=82.24476931396158",
        viewCounts: 0,
        createdAt: "2022-07-08T05:38:02.000Z",
        updatedAt: "2022-07-08T05:38:02.000Z",
        CategoryId: 3,
        Category: {
          id: 3,
          name: "義大利料理",
          createdAt: "2022-07-08T05:38:02.000Z",
          updatedAt: "2022-07-08T05:38:02.000Z",
        },
      },
      {
        id: 16,
        name: "Alene Mueller",
        tel: "140-306-0474",
        address: "9416 Jordyn Summit",
        opening_hours: "08:00",
        description: "voluptates occaecati explicabo",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=73.52380899939143",
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
      },
      {
        id: 17,
        name: "Savannah Bergstrom",
        tel: "931.876.8573 x32212",
        address: "022 Mckayla Pike",
        opening_hours: "08:00",
        description:
          "Odit et illo. Eveniet et sint voluptate molestiae non. Ad aut facilis est molestiae aut nemo.",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=66.77557146112049",
        viewCounts: 0,
        createdAt: "2022-07-08T05:38:02.000Z",
        updatedAt: "2022-07-08T05:38:02.000Z",
        CategoryId: 2,
        Category: {
          id: 2,
          name: "日本料理",
          createdAt: "2022-07-08T05:38:02.000Z",
          updatedAt: "2022-07-08T05:38:02.000Z",
        },
      },
      {
        id: 18,
        name: "Ivy Schroeder",
        tel: "617-878-6941",
        address: "381 Genesis Run",
        opening_hours: "08:00",
        description:
          "Laudantium a dolore laboriosam porro ut accusantium facere culpa aut. At accusamus dolor dolores neque. Aut excepturi quis quasi aperiam at unde. Ipsum quaerat rem qui. Deleniti labore odio.",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=17.02403826805936",
        viewCounts: 0,
        createdAt: "2022-07-08T05:38:02.000Z",
        updatedAt: "2022-07-08T05:38:02.000Z",
        CategoryId: 2,
        Category: {
          id: 2,
          name: "日本料理",
          createdAt: "2022-07-08T05:38:02.000Z",
          updatedAt: "2022-07-08T05:38:02.000Z",
        },
      },
      {
        id: 19,
        name: "Jordy Conn",
        tel: "375-244-6090 x25398",
        address: "1760 Hane Road",
        opening_hours: "08:00",
        description:
          "Vel quibusdam ea sequi adipisci distinctio eius. In ut quia dolor. Laboriosam facere saepe ratione esse ab. Qui accusantium dicta nesciunt aut aut sed. Iusto illum consequatur. Quae nisi nesciunt aut inventore et.",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=48.8747961916413",
        viewCounts: 0,
        createdAt: "2022-07-08T05:38:02.000Z",
        updatedAt: "2022-07-08T05:38:02.000Z",
        CategoryId: 3,
        Category: {
          id: 3,
          name: "義大利料理",
          createdAt: "2022-07-08T05:38:02.000Z",
          updatedAt: "2022-07-08T05:38:02.000Z",
        },
      },
      {
        id: 20,
        name: "Brooklyn Schmidt",
        tel: "777.365.5012",
        address: "8874 Pagac Shoals",
        opening_hours: "08:00",
        description:
          "Ea commodi corporis omnis. Aut consequatur aut fuga rerum. Harum nobis occaecati et quis. Nesciunt ratione omnis quo quia sit.\n \rOptio ducimus et id perferendis nam libero quasi eos et. Et enim sint assumenda nostrum molestias. Eaque ea et quidem vel maxime labore et quo dolorem.\n \rAutem dignissimos voluptatum aliquam itaque saepe eum voluptatum. Veritatis sed modi nihil qui perspiciatis sed aspernatur in perferendis. Veritatis qui aut repellendus corrupti et qui et illo. Est perferendis fugiat et neque nisi perspiciatis impedit qui. Non impedit enim provident accusantium quia. Illo accusamus repellendus totam corporis sunt.",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=81.83027784221397",
        viewCounts: 0,
        createdAt: "2022-07-08T05:38:02.000Z",
        updatedAt: "2022-07-08T05:38:02.000Z",
        CategoryId: 3,
        Category: {
          id: 3,
          name: "義大利料理",
          createdAt: "2022-07-08T05:38:02.000Z",
          updatedAt: "2022-07-08T05:38:02.000Z",
        },
      },
      {
        id: 21,
        name: "Elda Conroy",
        tel: "1-906-739-4945 x189",
        address: "942 Oberbrunner Springs",
        opening_hours: "08:00",
        description:
          "Dolore omnis voluptas et sint temporibus exercitationem incidunt deserunt enim. Cumque eligendi vero est. Architecto quia omnis. Placeat quia est. Minima quam at doloribus quia laboriosam asperiores pariatur voluptas culpa. Ipsa fugiat id alias reiciendis harum.\n \rTemporibus consequatur hic est ut libero. Earum nemo voluptates iusto. Quia omnis optio consequatur consequatur et est porro.\n \rVeritatis nesciunt qui voluptatem error. Dolorum aspernatur aut odit. Placeat voluptate dolore occaecati qui veniam sit commodi voluptatem. Saepe dicta magnam iste in voluptatem. Modi rerum doloribus.",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=21.581418316049007",
        viewCounts: 0,
        createdAt: "2022-07-08T05:38:02.000Z",
        updatedAt: "2022-07-08T05:38:02.000Z",
        CategoryId: 2,
        Category: {
          id: 2,
          name: "日本料理",
          createdAt: "2022-07-08T05:38:02.000Z",
          updatedAt: "2022-07-08T05:38:02.000Z",
        },
      },
      {
        id: 22,
        name: "Dejon Ledner",
        tel: "578-336-2443 x879",
        address: "66899 Nestor Centers",
        opening_hours: "08:00",
        description:
          "Eum nostrum quas recusandae. Officia eos ea aut enim dolorum explicabo a. Autem dolor amet veritatis et illo. Et similique debitis et. Distinctio et harum itaque. Rerum rerum perspiciatis autem aut id.",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=75.51997520073127",
        viewCounts: 0,
        createdAt: "2022-07-08T05:38:02.000Z",
        updatedAt: "2022-07-08T05:38:02.000Z",
        CategoryId: 3,
        Category: {
          id: 3,
          name: "義大利料理",
          createdAt: "2022-07-08T05:38:02.000Z",
          updatedAt: "2022-07-08T05:38:02.000Z",
        },
      },
      {
        id: 23,
        name: "Rozella Bins",
        tel: "169-485-9233 x317",
        address: "07964 Melvina Port",
        opening_hours: "08:00",
        description: "Qui ut aspernatur.",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=68.13202983003382",
        viewCounts: 0,
        createdAt: "2022-07-08T05:38:02.000Z",
        updatedAt: "2022-07-08T05:38:02.000Z",
        CategoryId: 3,
        Category: {
          id: 3,
          name: "義大利料理",
          createdAt: "2022-07-08T05:38:02.000Z",
          updatedAt: "2022-07-08T05:38:02.000Z",
        },
      },
      {
        id: 24,
        name: "Floy Marvin MD",
        tel: "(700) 779-1226",
        address: "567 Myra Green",
        opening_hours: "08:00",
        description: "Provident earum porro sed officiis.",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=87.5419878087297",
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
      },
      {
        id: 25,
        name: "Ellis Jast",
        tel: "1-213-029-2769",
        address: "1481 Blanda Turnpike",
        opening_hours: "08:00",
        description: "consequatur",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=26.221308083917606",
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
      },
      {
        id: 26,
        name: "Lila Dooley Jr.",
        tel: "343.431.7644",
        address: "613 Brakus Islands",
        opening_hours: "08:00",
        description: "id",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=89.35791903014893",
        viewCounts: 0,
        createdAt: "2022-07-08T05:38:02.000Z",
        updatedAt: "2022-07-08T05:38:02.000Z",
        CategoryId: 2,
        Category: {
          id: 2,
          name: "日本料理",
          createdAt: "2022-07-08T05:38:02.000Z",
          updatedAt: "2022-07-08T05:38:02.000Z",
        },
      },
      {
        id: 27,
        name: "Makayla Stroman",
        tel: "1-822-162-8190 x7604",
        address: "2340 Schroeder Springs",
        opening_hours: "08:00",
        description: "itaque",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=96.48708660747087",
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
      },
      {
        id: 28,
        name: "Citlalli West",
        tel: "1-964-260-8387 x4981",
        address: "4875 Gaston Stravenue",
        opening_hours: "08:00",
        description:
          "Eos magni vitae pariatur qui fuga. Nostrum et eveniet et ea sed vel minima ut eos. Ut iste ipsum.",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=75.38080820801059",
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
      },
      {
        id: 29,
        name: "Ernie Reinger",
        tel: "024-333-7562 x4240",
        address: "942 Bridget Rest",
        opening_hours: "08:00",
        description:
          "Quod ut doloremque. Eligendi aspernatur fugit qui non vitae molestiae porro. Nihil molestiae ullam et voluptatem sit dolorem.\n \rQuidem et quas voluptatibus rerum occaecati voluptatibus blanditiis. Esse assumenda est dolor. Sit quas odit perferendis. Quos unde officiis.\n \rDicta vel deserunt odit culpa molestiae atque. Et vitae maxime non quis praesentium quo voluptas reprehenderit. Asperiores ut omnis perferendis eaque nobis voluptas et at.",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=66.11952152931187",
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
      },
      {
        id: 30,
        name: "Henry Romaguera",
        tel: "660-520-5381",
        address: "0013 Hintz Course",
        opening_hours: "08:00",
        description:
          "Aliquid nobis officia modi architecto.\nQuia soluta eos vel fugiat et ratione.",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=83.7130256148287",
        viewCounts: 0,
        createdAt: "2022-07-08T05:38:02.000Z",
        updatedAt: "2022-07-08T05:38:02.000Z",
        CategoryId: 3,
        Category: {
          id: 3,
          name: "義大利料理",
          createdAt: "2022-07-08T05:38:02.000Z",
          updatedAt: "2022-07-08T05:38:02.000Z",
        },
      },
      {
        id: 31,
        name: "Betty Spinka",
        tel: "916-171-4570 x9630",
        address: "8791 Raymond Fords",
        opening_hours: "08:00",
        description:
          "Tempore aspernatur rem eveniet ratione minus rem. Vero labore facere sunt accusantium enim ut.",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=41.22280888116949",
        viewCounts: 0,
        createdAt: "2022-07-08T05:38:02.000Z",
        updatedAt: "2022-07-08T05:38:02.000Z",
        CategoryId: 2,
        Category: {
          id: 2,
          name: "日本料理",
          createdAt: "2022-07-08T05:38:02.000Z",
          updatedAt: "2022-07-08T05:38:02.000Z",
        },
      },
      {
        id: 32,
        name: "Cyrus Dickinson",
        tel: "772-174-4018 x6475",
        address: "9818 Brett Station",
        opening_hours: "08:00",
        description:
          "Tenetur aut non illum cum. Similique temporibus consequatur aut temporibus velit quisquam iusto. Sunt sit ipsum in voluptatibus et fuga architecto esse qui. Rerum molestiae consequatur consequatur doloremque sit est delectus magni. Eos tempore libero eaque ab quia in laudantium alias. Voluptatem voluptatem velit ipsam.",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=12.854397641657233",
        viewCounts: 0,
        createdAt: "2022-07-08T05:38:02.000Z",
        updatedAt: "2022-07-08T05:38:02.000Z",
        CategoryId: 2,
        Category: {
          id: 2,
          name: "日本料理",
          createdAt: "2022-07-08T05:38:02.000Z",
          updatedAt: "2022-07-08T05:38:02.000Z",
        },
      },
      {
        id: 33,
        name: "Sam Spencer",
        tel: "312-780-0347",
        address: "84943 Hills Burgs",
        opening_hours: "08:00",
        description: "fuga",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=92.58180601567983",
        viewCounts: 0,
        createdAt: "2022-07-08T05:38:02.000Z",
        updatedAt: "2022-07-08T05:38:02.000Z",
        CategoryId: 2,
        Category: {
          id: 2,
          name: "日本料理",
          createdAt: "2022-07-08T05:38:02.000Z",
          updatedAt: "2022-07-08T05:38:02.000Z",
        },
      },
      {
        id: 34,
        name: "Raheem Wilderman",
        tel: "(716) 940-3536 x69837",
        address: "66111 Paucek Cape",
        opening_hours: "08:00",
        description:
          "Autem voluptatem et blanditiis.\nMollitia rerum similique voluptates voluptatum eos accusantium.\nQui sit perspiciatis tempore sint accusamus eveniet vitae qui commodi.\nVelit eligendi occaecati expedita numquam nostrum.",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=94.2782909272089",
        viewCounts: 0,
        createdAt: "2022-07-08T05:38:02.000Z",
        updatedAt: "2022-07-08T05:38:02.000Z",
        CategoryId: 2,
        Category: {
          id: 2,
          name: "日本料理",
          createdAt: "2022-07-08T05:38:02.000Z",
          updatedAt: "2022-07-08T05:38:02.000Z",
        },
      },
      {
        id: 35,
        name: "Kyleigh Wyman",
        tel: "(977) 964-1705 x24467",
        address: "925 Sincere Villages",
        opening_hours: "08:00",
        description: "sint",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=32.33720774661586",
        viewCounts: 0,
        createdAt: "2022-07-08T05:38:02.000Z",
        updatedAt: "2022-07-08T05:38:02.000Z",
        CategoryId: 2,
        Category: {
          id: 2,
          name: "日本料理",
          createdAt: "2022-07-08T05:38:02.000Z",
          updatedAt: "2022-07-08T05:38:02.000Z",
        },
      },
      {
        id: 36,
        name: "Nathen Blick",
        tel: "632-454-0092 x1466",
        address: "11411 Kemmer Rest",
        opening_hours: "08:00",
        description: "aperiam",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=14.495255620429859",
        viewCounts: 0,
        createdAt: "2022-07-08T05:38:02.000Z",
        updatedAt: "2022-07-08T05:38:02.000Z",
        CategoryId: 2,
        Category: {
          id: 2,
          name: "日本料理",
          createdAt: "2022-07-08T05:38:02.000Z",
          updatedAt: "2022-07-08T05:38:02.000Z",
        },
      },
      {
        id: 37,
        name: "Pink Miller",
        tel: "1-902-914-7695 x0565",
        address: "73249 Grady Mountain",
        opening_hours: "08:00",
        description:
          "Est voluptatem eveniet dolorum aut temporibus aut officiis dolorum. Eos dolorum illum dolore aspernatur veniam aut. Velit aspernatur et rem illo ad accusamus laudantium. Sed aut hic delectus quas omnis impedit. Dignissimos tempore aut sequi quidem praesentium nobis.\n \rQui dolorum porro minima sapiente quibusdam quidem explicabo. Harum voluptas sint cupiditate corrupti aliquid est necessitatibus est suscipit. Amet nisi voluptas aut impedit. Sunt impedit sed. Hic quisquam debitis sint alias.\n \rRerum facere dolorum recusandae tenetur maxime. Est nulla alias voluptatem dolorem nesciunt tempora et. Numquam occaecati repudiandae. Corporis placeat quia expedita.",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=56.70667882668059",
        viewCounts: 0,
        createdAt: "2022-07-08T05:38:02.000Z",
        updatedAt: "2022-07-08T05:38:02.000Z",
        CategoryId: 3,
        Category: {
          id: 3,
          name: "義大利料理",
          createdAt: "2022-07-08T05:38:02.000Z",
          updatedAt: "2022-07-08T05:38:02.000Z",
        },
      },
      {
        id: 38,
        name: "Layla Cruickshank",
        tel: "260-391-8096",
        address: "9573 Herzog Squares",
        opening_hours: "08:00",
        description: "ea quis rerum",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=8.248137467912198",
        viewCounts: 0,
        createdAt: "2022-07-08T05:38:02.000Z",
        updatedAt: "2022-07-08T05:38:02.000Z",
        CategoryId: 2,
        Category: {
          id: 2,
          name: "日本料理",
          createdAt: "2022-07-08T05:38:02.000Z",
          updatedAt: "2022-07-08T05:38:02.000Z",
        },
      },
      {
        id: 39,
        name: "Kelli Denesik DDS",
        tel: "(150) 647-8636",
        address: "96326 Mertie Fords",
        opening_hours: "08:00",
        description:
          "Libero aut deleniti odit et officia aut ratione eius. Labore omnis quasi a enim qui dolorem. Possimus ab et doloribus.\n \rMolestias nisi totam velit dicta possimus excepturi. Nihil porro reprehenderit dolore. Qui optio rerum iusto sed. Qui ea perspiciatis animi. Quia eum voluptates.\n \rEa vel cum. Autem soluta et expedita adipisci velit qui quia nihil nihil. Debitis natus id possimus. Rerum libero dolores excepturi odio.",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=96.5121726338109",
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
      },
      {
        id: 40,
        name: "Gail Koch Sr.",
        tel: "(759) 449-6808 x25255",
        address: "906 Demario Mall",
        opening_hours: "08:00",
        description: "enim",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=24.075863002545272",
        viewCounts: 0,
        createdAt: "2022-07-08T05:38:02.000Z",
        updatedAt: "2022-07-08T05:38:02.000Z",
        CategoryId: 2,
        Category: {
          id: 2,
          name: "日本料理",
          createdAt: "2022-07-08T05:38:02.000Z",
          updatedAt: "2022-07-08T05:38:02.000Z",
        },
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
        Category: {
          id: 1,
          name: "中式料理",
          createdAt: "2022-07-08T05:38:02.000Z",
          updatedAt: "2022-07-08T05:38:02.000Z",
        },
      },
      {
        id: 42,
        name: "Elenora Runolfsson",
        tel: "269-550-1482 x854",
        address: "98315 Nikolaus Crest",
        opening_hours: "08:00",
        description:
          "Repellat eius aut voluptates inventore illo animi non. Et aut sit vitae architecto. Esse natus vitae fugit sint in nesciunt consequuntur quam fugit.",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=76.32462170543035",
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
      },
      {
        id: 43,
        name: "Audreanne Ward",
        tel: "965-658-8223 x3855",
        address: "61015 Dietrich Circles",
        opening_hours: "08:00",
        description:
          "Id non quas optio qui a. Rerum facilis perferendis iure quia. Molestiae eum maiores quis quia neque dicta. Facere esse exercitationem quasi porro laudantium aspernatur esse rerum. Adipisci reiciendis sunt.\n \rAut hic voluptate sint et sit sed. Nam modi id sed similique rerum ut exercitationem. Sequi facere rem eum sequi quisquam nihil. Et dolorem dicta. Dolor soluta quo error ea sint repudiandae. Sit quibusdam velit exercitationem explicabo ex omnis qui.\n \rNostrum impedit qui et. Repellendus ipsum sunt quia voluptas eaque enim sunt aliquid aut. Nemo ullam voluptatem.",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=98.12452595686247",
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
      },
      {
        id: 44,
        name: "Alek Dooley",
        tel: "824.020.9809",
        address: "96020 Sawayn Keys",
        opening_hours: "08:00",
        description:
          "Modi quis voluptatem et labore dolorum ullam. Consequuntur harum corrupti est. Est praesentium et asperiores ut. Nihil praesentium animi odit assumenda.",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=10.032549212094644",
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
      },
      {
        id: 45,
        name: "Lesley Reilly",
        tel: "358.905.7411",
        address: "4789 Purdy Square",
        opening_hours: "08:00",
        description:
          "Impedit aliquam perspiciatis. Sed molestias quibusdam voluptatem possimus iusto amet. Quo inventore voluptatem. Quae et fugit fugiat pariatur eos et quae id. Quas nulla et nisi soluta quasi deserunt.",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=68.09118344813258",
        viewCounts: 0,
        createdAt: "2022-07-08T05:38:02.000Z",
        updatedAt: "2022-07-08T05:38:02.000Z",
        CategoryId: 3,
        Category: {
          id: 3,
          name: "義大利料理",
          createdAt: "2022-07-08T05:38:02.000Z",
          updatedAt: "2022-07-08T05:38:02.000Z",
        },
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
        Category: {
          id: 2,
          name: "日本料理",
          createdAt: "2022-07-08T05:38:02.000Z",
          updatedAt: "2022-07-08T05:38:02.000Z",
        },
      },
      {
        id: 47,
        name: "Harmon Kuhn PhD",
        tel: "342-389-7219 x899",
        address: "67602 Gutkowski Tunnel",
        opening_hours: "08:00",
        description:
          "Similique aperiam qui dicta et consectetur voluptatum enim.\nDolores dolorem numquam sit cumque sed est et rem dolor.",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=43.20310477250855",
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
        Category: {
          id: 4,
          name: "墨西哥料理",
          createdAt: "2022-07-08T05:38:02.000Z",
          updatedAt: "2022-07-08T05:38:02.000Z",
        },
      },
      {
        id: 49,
        name: "Trace Barton",
        tel: "1-970-228-3927 x87273",
        address: "451 Gerlach Mountains",
        opening_hours: "08:00",
        description:
          "Aut ad at reprehenderit iure cum corrupti optio voluptatibus velit.",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=1.6287841142439197",
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
      },
      {
        id: 50,
        name: "Elza Rolfson",
        tel: "380-904-3024 x067",
        address: "980 Bruen Squares",
        opening_hours: "08:00",
        description:
          "Ratione labore est accusantium saepe est repellendus. Recusandae amet consequatur ut. Debitis totam sint sit ut placeat consequatur voluptatem hic rerum.",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=32.902975919022445",
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
      },
    ],
  };

export default {
  data() {
    return {
      restaurants: [],
    };
  },
  created() {
    this.fetchRestaurants();
  },
  methods: {
    fetchRestaurants() {
      this.restaurants = dummyData.restaurants;
    },
    deleteRestaurant(restaurantId) {
      this.restaurants = this.restaurants.filter(
        (restaurant) => restaurant.id !== restaurantId
      );
    },
  },
};
</script>