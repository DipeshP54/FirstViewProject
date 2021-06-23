<template>
  <form
    class="create-post-panel"
    @submit.prevent="createNewPost"
    :class="{ '--exceeded': newPostCharCount > 200 }"
  >
    <label for="txtPost">
      <strong>New Post : </strong>({{ newPostCharCount }}/200)
    </label>
    <textarea id="txtpost" rows="5" v-model="newPostContent" />

    <div class="create-post-panel_submit">
      <div class="create-post-type">
        <label for="ddlPostType"><strong>Post Type : </strong></label>

        <select id="ddlPostType" v-model="newPostType">
          <option
            v-for="(opt, index) in postTypes"
            :key="index"
            :value="opt.value"
          >
            {{ opt.typeName }}
          </option>
        </select>
      </div>

      <button :disabled="newPostCharCountOverLimit">Post It!</button>
    </div>
  </form>
</template>

<script>
export default {
  name: "CreatePostPanel",
  data() {
    return {
      newPostContent: "",
      newPostType: "instant",
      postTypes: [
        { value: "draft", typeName: "Draft" },
        { value: "instant", typeName: "Instant" },
      ],
    };
  },
  computed: {
    newPostCharCount() {
      return this.newPostContent.length;
    },
    newPostCharCountOverLimit() {
      return this.newPostContent.length > 200;
    },
  },
  methods: {
    createNewPost() {
      if (this.newPostContent && this.newPostType !== "draft") {
        this.$emit("add-post", this.newPostContent);
        this.newPostContent = "";
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.create-post-panel {
  padding-top: 20px;
  display: flex;
  flex-direction: column;

  textarea {
    border: 1px solid #dfe3e8;
    border-radius: 5px;
  }

  .create-post-panel_submit {
    display: flex;
    justify-content: space-between;

    .create-post-type {
      padding: 10px 0;
    }

    button {
      padding: 5px 20px;
      margin: auto 0;
      border-radius: 5px;
      border: none;
      background-color: indigo;
      color: white;
      font-weight: bold;
    }
  }

  &.--exceeded {
    color: red;
    border-color: red;

    .create-post-panel_submit {
      button {
        background-color: red;
        color: white;
      }
    }
  }
}
</style>