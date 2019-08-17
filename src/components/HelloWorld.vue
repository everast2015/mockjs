<template>
  <div class="hello">
    <div :key="index" v-for="(item,index) in datalist">{{index}}-{{item.title}}</div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      datalist: [],
    }
  },
  props: {
    msg: String,
  },
  mounted() {
    this.$http.get('/posts').then(res => {
      console.log(res.data.posts)
      this.datalist = res.data.posts
    })
  },
}
</script>
