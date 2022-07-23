<template>
  <form @submit.stop.prevent="handleSubmit">
    <div class="form-group mb-4">
      <label for="text">留下評論：</label>
      <textarea v-model="text" class="form-control" rows="3" name="text" />
    </div>
    <div class="d-flex align-items-center justify-content-between">
      <button type="button" class="btn btn-link" @click="$router.back()">
        回上一頁
      </button>
      <button type="submit" class="btn btn-primary mr-0">Submit</button>
    </div>
  </form>
</template>

<script>
import commentsAPI from "./../apis/comments";
import { Toast } from "./../utils/helpers";

export default {
  props: {
    restaurantId: {
      type: Number,
      required: true,
    },
  },

  data() {
    return {
      text: "",
    };
  },
  methods: {
    async handleSubmit() {
      try {
        // 避免輸入空評論
        if (!this.text.trim()) {
          Toast.fire({
            icon: "error",
            title: "請輸入餐廳評論內容",
          });
          return;
        }
        this.isProcessing = true;
        const { data } = await commentsAPI.createComments({
          restaurantId: this.restaurantId,
          text: this.text,
        });

        this.$emit("after-create-comment", {
          commentId: data.commentId, // 尚未串接 API 暫時使用隨機的 id
          restaurantId: this.restaurantId,
          text: this.text,
        });

        this.isProcessing = false;
        this.text = ""; // 將表單內的資料清空
      } catch (error) {
        Toast.fire({
          icon: "error",
          title: "無法新增餐廳評論，請稍後再試",
        });
      }
    },
  },
};
</script>