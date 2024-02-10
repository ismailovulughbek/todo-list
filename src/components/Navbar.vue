<template>
  <header class="header">
    <Transition name="header-navbar">
      <nav class="header-navbar" v-show="header">
        <button
          class="header-navbar__lang"
          @click="changeLang"
          v-if="lang == 'uz'"
        >
          {{ words.navbar.langBtn[lang] }}
        </button>
        <button class="header-navbar__lang" @click="changeLang" v-else>
          {{ words.navbar.langBtn[lang] }}
        </button>
        <h2 class="header-navbar__title">{{ words.navbar.title[lang] }}</h2>
        <button class="header-navbar__search" @click="header = false">
          <img src="@/assets/img/search.svg" alt="" />
        </button>
      </nav>
    </Transition>
    <Transition name="header-search">
      <div class="header-search" v-show="!header">
        <button class="header-search__btn" @click="header = true">
          <img src="@/assets/img/back.svg" alt="" />
        </button>
        <input
          type="text"
          :placeholder="words.navbar.placeholder[lang]"
          v-model="searchValue"
          class="header-search__input"
        />
        <button class="header-search__btn" @click="searchValue = ''">
          <img src="@/assets/img/clear.svg" alt="" />
        </button>
      </div>
    </Transition>
  </header>
</template>

<script>
export default {
  name: "Navbar",
  props: {
    lang: String,
  },
  data() {
    return {
      header: true,
      searchValue: "",
      words: {},
    };
  },
  created() {
    this.words = JSON.parse(localStorage.langWords);
  },
  methods: {
    changeLang() {
      this.$emit("changeLang", this.lang == "uz" ? "ru" : "uz");
    },
  },
  watch: {
    searchValue(value) {
      this.$emit("search", value);
    },
  },
};
</script>
