<template>
  <div class="container">
    <form class="box">
      <b-field label="Name" label-position="on-border">
        <b-input v-model="name"/>
      </b-field>
      <b-field label="Username" label-position="on-border">
        <b-input v-model="username"/>
      </b-field>
      <b-button type="is-success" @click="saved">Save</b-button>
    </form>
  </div>
</template>
<script>
export default {
  props: ['input'],
  data:()=>({
    name: '',
    username: ''
  }),
  created(){
    this.name = this.input.name
    this.username = this.input.username
  },
  methods:{
    saved(){
      this.$emit('update',{
        name : this.name,
        username: this.username
      })
    }
  },
  watch:{
    input:{
      handler(newvalue){
        this.name = newvalue.name
        this.username = newvalue.username
      },  
      deep: true
    }
  }
}
</script>

