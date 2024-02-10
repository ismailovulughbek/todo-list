<template>
  <Navbar :lang="lang" @changeLang="changeLang" @search="search = $event" />
  <Notes
    :notes="notesFilter"
    :lang="lang"
    @changeNote="changeNote"
    @delNote="delNote"
  />
  <Modal
    v-if="openModal"
    :edit="edit"
    :editNote="editNote"
    @closeModal="closeModal"
    @addNote="addNote"
    @editedNote="editedNote"
  />
  <AddButton @modalOpen="modalOpen" />
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import Notes from "@/components/Notes.vue";
import AddButton from "@/components/AddButton.vue";
import Modal from "@/components/Modal.vue";
import langWords from "@/lang";
export default {
  name: "App",
  components: {
    Navbar,
    Notes,
    AddButton,
    Modal,
  },
  data() {
    return {
      lang: "uz",
      notes: [],
      openModal: false,
      edit: false,
      editNote: {},
      search: "",
    };
  },
  created() {
    this.getNotes();
    localStorage.lang = localStorage.lang || "uz";
    this.lang = localStorage.lang || "uz";
    localStorage.langWords = JSON.stringify(langWords);
  },
  methods: {
    changeLang(value) {
      this.lang = localStorage.lang = value;
    },
    modalOpen() {
      this.openModal = true;
      this.edit = false;
    },
    closeModal() {
      this.openModal = false;
      this.edit = false;
    },
    changeNote(id) {
      this.openModal = true;
      this.edit = true;

      let pickedNote = this.notes.find((note) => note.id == id);
      this.editNote = pickedNote;
    },
    addNote(obj) {
      if (obj.title != "" && obj.descr != "") {
        this.notes.push(obj);
      }
    },
    editedNote(obj) {
      this.notes.forEach((note) => {
        if (note.id == obj.id) {
          note.title = obj.title;
          note.descr = obj.descr;
          note.date = obj.date;
        }
      });
    },
    delNote(id) {
      let index = this.notes.findIndex((note) => note.id == id);
      this.notes.splice(index, 1);
    },
    getNotes() {
      let localNotes = localStorage.getItem("notes");
      if (localNotes) {
        this.notes = JSON.parse(localNotes);
      }
    },
  },
  computed: {
    notesFilter() {
      return this.search
        ? this.notes.filter((item) =>
            item.title.toLowerCase().includes(this.search.toLowerCase())
          )
        : this.notes;
    },
  },
  watch: {
    notes: {
      handler() {
        localStorage.setItem("notes", JSON.stringify(this.notes));
      },
      deep: true,
    },
  },
};
</script>

<style></style>
