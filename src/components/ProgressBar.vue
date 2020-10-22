<template>
  <div>
    <v-progress-linear v-model="amountCompleted" height="25">
      <strong>{{ Math.ceil(amountCompleted) }}% completed</strong>
    </v-progress-linear>
  </div>
</template>

<script>
export default {
  name: "ProgressBar",
  props: ["amountCompleted"],
};
</script>