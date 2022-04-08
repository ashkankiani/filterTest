<template>
  <div class="col-12">
    <div class="card mb-3">
      <slot name="title"></slot>
      <div class="card-body d-flex align-items-center justify-content-start">
        <slot name="inputData"></slot>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "slotCardHeader"
};
</script>

<style scoped></style>
