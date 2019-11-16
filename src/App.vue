<template>
  <div class="container">
    <section class="hero is-primary">
      <div class="hero-body">
        <div class="container">
          <h1 class="title">{{title}}</h1>
          <h2 class="subtitle">{{name}}</h2>
        </div>
      </div>
    </section>
    <div class="container">
      <div class="buttons">
        <b-button
          v-if="mode !== 'setting'"
          icon-left="account"
          @click="mode = 'setting'"
          type="is-dark"
        >Setting</b-button>
        <b-button
          v-if="mode !== 'list'"
          icon-left="format-list-bulleted"
          @click="mode = 'list'"
          type="is-info"
        >List</b-button>
        <b-button
          v-if="mode !== 'mutate'"
          icon-left="plus-thick"
          @click="mode = 'mutate'"
          type="is-primary"
        >Add</b-button>
      </div>
      <setting v-if="mode == 'setting'" :input="{name:name, username:username}" @update="userset"/>
      <list v-if="mode == 'list'" :lists="lists"/>
      <mutate v-if="mode == 'mutate'" v-model="value" @save="saving"/>
    </div>
  </div>
</template>
<script>
import setting from "./components/setting";
import list from "./components/list";
import mutate from "./components/mutate";
export default {
  components: {
    setting,
    list,
    mutate
  },
  data: () => ({
    mode: "list",
    lists: [],
    value: {
      title: "",
      article: ""
    },
    name: "Marie Danilene Bulosan",
    title: "Blog",
    username: "marie_biskit"
  }),
  methods: {
    saving(mode = "") {
      if (mode === "cancel") this.mode = "list";
      else {
        this.value["created"] = moment().format("YYYY-MM-DD");
        this.value["name"] = this.name;
        this.value["username"] = this.username;
        this.lists.push(this.value);
        this.value = {
          title: "",
          article: ""
        };
        this.mode = "list";
      }
    },
    userset(user) {
      this.name = user.name;
      this.username = user.username;
      this.mode = list;
    }
  }
};
</script>
<style scoped>
.buttons {
  margin: 10px;
  text-align: center;
}
.buttons button {
  margin: 0 auto;
}
</style>
