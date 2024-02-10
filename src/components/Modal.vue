<template>
  <div class="modal">
    <div class="modal__block">
      <h2 class="modal__title">
        {{ edit ? "Eslatma Tahrirlash" : "Eslatma Qo'shish" }}
      </h2>
      <div class="modal__inputs">
        <label>
          <span>Sarlovxa</span>
          <input type="text" placeholder="Sarlovxa.." v-model="title" />
        </label>
        <label>
          <span>Content</span>
          <textarea placeholder="Content" v-model="descr"></textarea>
        </label>
      </div>
      <div class="modal__btns">
        <button class="modal__btn modal__close" @click="closeModal">
          Bekor Qilish
        </button>
        <button class="modal__btn modal__add" v-if="!edit" @click="addNote">
          Qo'shish
        </button>
        <button class="modal__btn modal__edit" v-else @click="editedNote">
          O'zgartirish
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import { v4 as uuidv4 } from "uuid";
export default {
  name: "Modal",
  props: {
    edit: Boolean,
    editNote: Object,
  },
  data() {
    return {
      title: "",
      descr: "",
    };
  },
  created() {
    if (this.edit) {
      this.title = this.editNote.title;
      this.descr = this.editNote.descr;
    }
  },
  methods: {
    closeModal() {
      this.$emit("closeModal");
    },
    addNote() {
      if (this.title != "" && this.descr != "") {
        const add = {
          id: uuidv4(),
          title: this.title,
          descr: this.descr,
          date: new Date().toLocaleDateString(),
        };
        this.$emit("addNote", add);
        this.closeModal();
      } else {
        alert("Eslatma qo'shish uchun Sarlovha va Content ni to'ldiring");
      }
    },
    editedNote() {
      if (this.title != "" && this.descr != "") {
        const edit = {
          id: this.editNote.id,
          title: this.title,
          descr: this.descr,
          date: new Date().toLocaleDateString(),
        };
        this.$emit("editedNote", edit);
        this.closeModal();
      } else {
        alert("Eslatma o'zgartirish uchun Sarlovha va Content ni to'ldiring");
      }
    },
  },
};
</script>
