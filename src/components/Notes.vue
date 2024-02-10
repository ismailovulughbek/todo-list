<template>
  <div class="notes">
    <div class="container">
      <div class="notes-top">
        <h2 class="notes-top__title">{{ words.notes.title[lang] }}</h2>
        <button class="notes-top__button" @click="grid = !grid">
          <img src="@/assets/img/list.svg" alt="" v-if="grid" />
          <img src="@/assets/img/grid.svg" alt="" v-else />
          <span>
            {{ grid ? words.notes.list[lang] : words.notes.grid[lang] }}
          </span>
        </button>
      </div>
      <h2 class="notes-title" v-if="!notes.length">
        {{ words.notes.notFound[lang] }}
      </h2>
      <div class="notes-list" :class="{ grid: !grid }">
        <NotesItem
          v-for="note in notes"
          :key="note.id"
          :note="note"
          :grid="grid"
          @changeNote="$emit('changeNote', note.id)"
          @delNote="$emit('delNote', note.id)"
        />
      </div>
    </div>
  </div>
</template>

<script>
import NotesItem from "@/components/NotesItem.vue";

export default {
  name: "Notes",
  props: {
    notes: Array,
    lang: String,
  },
  components: {
    NotesItem,
  },
  data() {
    return {
      grid: true,
      words: {},
    };
  },
  created() {
    this.words = JSON.parse(localStorage.langWords);
  },
};
</script>
