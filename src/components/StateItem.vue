<template>
  <div class = "block has-text-centered">
    <div class = "button is-primary is-normal" @click="$emit('clicked',this.data)">{{data}}</div>
  </div>
</template>

<script>
export default {
  name: 'StateItem',
  emits: ['clicked'],
  setup(props, ctx) {
    ctx.emit('clicked')
  },
  props: {
    data: String
  }
  // methods:{
  //   onClickButton(event){
  //     this.$emit('clicked',this.data)
  //   }
  // }
}
</script>
