<template>
  <button class="add-btn" @click="$emit('modalOpen')">
    <img src="@/assets/img/pencil.svg" alt="" />
  </button>
</template>

<script>
export default {
  name: "AddButton",
};
</script>

<style lang="scss">
.add-btn {
  background: linear-gradient(
      0deg,
      rgba(103, 80, 164, 0.11),
      rgba(103, 80, 164, 0.11)
    ),
    #fffbfe;
  border-radius: 16px;
  box-shadow: 0px 4px 8px 3px rgba(0, 0, 0, 0.15);
  filter: drop-shadow(0px 1px 3px rgba(0, 0, 0, 0.3));
  width: 56px;
  height: 56px;
  display: flex;
  align-items: center;
  justify-content: center;
  position: fixed;
  bottom: 30px;
  right: 30px;
}
</style>
