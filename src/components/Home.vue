<template>
  <div class="home">
    <b-container class="product-details">
      <!-- <b-col class="block__element--modifier">test</b-col> -->
      <b-row>
        <b-col cols="5">
          <b-row>
            <p>Cap Toe Sneaker</p>
          </b-row>
          <b-row>
            <span><i class="fa fa-plus"></i>Add Season</span>
            <span v-if="seen"><i class="fa fa-plus"></i>Add Label</span>
          </b-row>
        </b-col>
        <b-col cols="7">
          <span>Idea</span>
          <span>In Development</span>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
export default {
  name: 'Home',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
  .block {
    &__element {
      &--modifier {
        color: green;
      }
    }
  }
</style>
