<template>
  <section class = "hero">
    <div class = "hero">
      <div class="block title">
        <h1 class="has-text-grey has-text-centered">{{ msg }}</h1>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
</script>
