<template>
  <div class="container">
    <form class="box">
      <b-field label="Title" label-position="on-border">
        <b-input v-model="title"/>
      </b-field>
      <b-field label="Article" label-position="on-border">
        <b-input type="textarea" v-model="article"/>
      </b-field>
      <b-button type="is-success" class="is-pulled-right" @click="saved">Save</b-button>
      <b-button type="is-danger" outlined @click="cancel">Cancel</b-button>
    </form>
  </div>
</template>
<script>
export default {
  props: ["value"],
  data: () => ({
    title: "",
    article: ""
  }),
  methods: {
    cancel() {
      this.title = "";
      this.article = "";
      this.$emit("save", "cancel");
    },
    saved() {
      this.$emit("save");
    }
  },
  watch: {
    title(newvalue) {
      this.$emit("input", { title: newvalue, article: this.article });
    },
    article(newvalue) {
      this.$emit("input", { title: this.title, article: newvalue });
    }
  }
};
</script>

