<template>
  <!-- <img :src="require('../assets/images/' + activity.image + '.png')" alt="Placeholder image"> -->
  <section class = "hero">
    <div class = "hero">
      <div class="block title">
        <h1 class="has-text-primary has-text-centered">{{activity.activity}}</h1>
      </div>
    </div>
  </section>
  <div class = "block"></div>
  <section>
    <div class="block has-text-centered">
      <h3>{{activity.instructions}}</h3>
    </div>
    <div class = "block"></div>
    <div class = "block has-text-centered">
      <a v-if="activity.link" class = "button is-primary" :href = "activity.link" target = "_blank">Start</a>
    </div>
  </section>
</template>

<script>
export default {
  name: 'ActivityItem',
  props: {
    activity: Object
  }
}
</script>
