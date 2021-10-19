<template>
  <div class="demo">
    <h2>{{ msg }}</h2>
    <h1>{{ val }}</h1>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String,
    val: Number
  }
}
</script>