<template>
  <div class="notes-item">
    <div class="notes-item__top" :class="{ between: !grid }">
      <h3 class="notes-item__title">{{ note.title }}</h3>
      <p class="notes-item__date">{{ note.date }}</p>
    </div>
    <p class="notes-item__descr">
      {{ note.descr }}
    </p>
    <div class="notes-item__btns">
      <button
        class="notes-item__btn notes-item__btn_edit"
        @click="$emit('changeNote')"
      >
        <img src="@/assets/img/pencil.svg" alt="" />
        <span>O'zgartirish</span>
      </button>
      <button class="notes-item__btn notes-item__btn_del" @click="$emit('delNote')">
        <img src="@/assets/img/del.svg" alt="" />
        <span>O'chirish</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "NotesItem",
  props: {
    note: Object,
    grid: Boolean,
  },
};
</script>
