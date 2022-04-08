<template>
  <div class="card mb-4 position-relative">
    <div class="card-body pt-4">
      <slot name="title"></slot>
      <slot name="inputData"></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "slotCard",
};
</script>

<style scoped></style>
