<template>
  <div class="item">
    <input
        type="checkbox"
        class="checkbox"
        v-bind:checked="this.isDone"
        @change="$emit('do-item')"
    />
    <span>{{ label }}</span>
    <button v-on:click="$emit('delete-item')">Remove</button>
  </div>
</template>

<script>
	export default {
        name: 'Item',
        props: {
            label: String,
            isDone: Boolean
        }
    }
</script>

<style src="@/assets/base.css"></style>