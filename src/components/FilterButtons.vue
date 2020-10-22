<template>
  <div>
    <button class="btn" @click="$emit('filter-reset')">All</button>
    <button class="btn" @click="$emit('filter-active')">Active</button>
    <button class="btn" @click="$emit('filter-completed')">Completed</button>
  </div>
</template>

<script>
export default {
  name: "FilterButtons",
};
</script>
