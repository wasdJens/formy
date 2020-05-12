<template>
  <div>
    <div class="column side">
      <slot name="left-content"></slot>
    </div>

    <div class="column middle">
      <slot name="middle-content"></slot>
    </div>

    <div class="column side">
      <slot name="right-content"></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "Layout"
};
</script>

<style lang="scss">
.column {
  float: left;
}

.column.side {
  width: 25%;
}

.column.middle {
  width: 50%;
}
</style>
