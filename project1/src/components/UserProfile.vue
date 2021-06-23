<template>
  <div class="user-profile">
    <div class="user-profile_sidebar">
      <div class="user-profile_user-panel">
        <h1 class="user-profile_userName">@{{ user.userName }}</h1>
        <div class="user-profile_admin-badge" v-if="user.isAdmin">Admin</div>
        <div class="use-profile_follower-count">
          <strong>Follwers: </strong> {{ followers }}
        </div>
      </div>
      <CreatePostPanel @add-post="addPost" />
    </div>
    <div class="user-profile_posts-wrapper">
      <PostItem
        v-for="disc in user.posts"
        :key="disc.id"
        :username="user.userName"
        :post="disc"
        @liked="toggleLiked"
      />
    </div>
  </div>
</template>

<script>
import PostItem from "./PostItem.vue";
import CreatePostPanel from "./CreatePostPanel.vue";

export default {
  name: "UserProfile",
  components: { CreatePostPanel, PostItem },
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        userName: "_DominicParker",
        firstName: "Dominic",
        lastName: "Parker",
        email: "dominic.parker@project1.com",
        isAdmin: true,
        posts: [
          {
            id: 1,
            content: "This is my first post.",
          },
          {
            id: 2,
            content: "This is my second post.",
          },
          {
            id: 3,
            content: "This is my Third post.",
          },
        ],
      },
    };
  },
  methods: {
    addPost(post) {
      this.user.posts.unshift({
        id: this.user.posts.length + 1,
        content: post,
      });
    },
  }
};
</script>


<style lang="scss" scoped>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  grid-gap: 50px;
  padding: 50px 5%;

  .user-profile_user-panel {
    display: flex;
    flex-direction: column;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #dfe3e8;
    margin-bottom: auto;

    h1 {
      margin: 0;
    }

    .user-profile_admin-badge {
      background: rebeccapurple;
      color: white;
      border-radius: 5px;
      margin-right: auto;
      padding: 0 10px;
      font-weight: bold;
    }
  }

  .user-profile_posts-wrapper {
    display: grid;
    grid-gap: 10px;
    margin-bottom: auto;
  }
}

//npm install [package-name]@[version-number]
</style>