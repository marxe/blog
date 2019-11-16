<template>
  <div class="container">
    <div class="card" v-for="(list, key) in lists" :key="key">
      <div class="card-content">
        <div class="media">
          <div class="media-content">
            <p class="title is-4">{{list.name}}</p>
            <p class="subtitle is-6">@{{list.username}}</p>
          </div>
        </div>

        <div class="content">
          {{list.article}}
          <br>
          <time :datetime="list.created">{{list.created}}</time>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: ["lists"]
};
</script>
