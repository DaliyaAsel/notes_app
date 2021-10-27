<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="container">
          <!--блок для выводв ошибки, если title пуст, вставили компонент message или  <message></message> -->
          <message v-if="message" :message="message" />

          <!--компонент для добавления заметки-->
          <newNote :note="note" @addNote="addNote" />
          <!--@addNote - 'это назване текущего emit, а через = "что мы будем делать, когда будет передаваться emit"-->

          <!--иконки svg-->
          <div class="note-header" style="margin: 36px 0">
            <h1>{{ title }}</h1>
            <!-- Search -->
            <search
              :value="search"
              placeholder="Find your note"
              @search="search = $event"
            />
            <div class="icons">
              <svg
                :class="{ active: grid }"
                @click="grid = true"
                style="cursor: pointer"
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <rect x="3" y="3" width="7" height="7"></rect>
                <rect x="14" y="3" width="7" height="7"></rect>
                <rect x="14" y="14" width="7" height="7"></rect>
                <rect x="3" y="14" width="7" height="7"></rect>
              </svg>
              <svg
                :class="{ active: !grid }"
                @click="grid = false"
                style="cursor: pointer"
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <line x1="8" y1="6" x2="21" y2="6"></line>
                <line x1="8" y1="12" x2="21" y2="12"></line>
                <line x1="8" y1="18" x2="21" y2="18"></line>
                <line x1="3" y1="6" x2="3" y2="6"></line>
                <line x1="3" y1="12" x2="3" y2="12"></line>
                <line x1="3" y1="18" x2="3" y2="18"></line>
              </svg>
            </div>
          </div>

          <!--notes - компонент для добавления заметки в массив заметок-->
          <notes :notes="notesFilter" @remove="removeNote" :grid="grid" />
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import message from "@/components/Message.vue";
import notes from "@/components/Notes.vue";
import newNote from "@/components/NewNote.vue";
import search from "@/components/Search.vue";

export default {
  components: {
    message,
    notes,
    newNote,
    search,
  },
  data() {
    return {
      title: "Notes App",
      search: "",
      message: null,
      grid: true,
      note: {
        title: "",
        selectPriotity: "default-priority",
        descr: "",
      },
      notes: [
        {
          title: "First note",
          descr: "Description for first note",
          selectPriotity: "default-priority",
          date: new Date().toLocaleString(),
        },
        {
          title: "Second note",
          descr: "Description for second note",
          selectPriotity: "default-priority",
          date: new Date().toLocaleString(),
        },
        {
          title: "Third note",
          descr: "Description for third note",
          selectPriotity: "default-priority",
          date: new Date().toLocaleString(),
        },
      ],
    };
  },
  computed: {
    notesFilter() {
      let array = this.notes,
        search = this.search;
      if (!search) return array; //если search пуст, то вернем массив просто
      search = search.trim().toLowerCase(); //избавились от пробелов и приравняли search к нижнему регистру
      // Filter
      array = array.filter(function (item) {
        if (item.title.toLowerCase().indexOf(search) !== -1) {
          return item;
        }
      });
      //Error
      return array;
    },
  },

  methods: {
    addNote() {
      let { title, descr, selectPriotity } = this.note;
      if (title === "") {
        this.message = "title can't be blank";
        return false;
      }
     
      this.notes.push({
        title,
        descr,
        selectPriotity,
        date: new Date().toLocaleString(),
      });

      this.message = null; //если заметка отправилась, то убираем сообщение об ошибке
      this.note.title = ""; //очищаем title
      this.note.descr = ""; //очищаем descr
      this.note.selectPriotity = "default-priority";
    },
    removeNote(index) {
      //удаление заметки из списка
      this.notes.splice(index, 1);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased; /*сглаживание шрифтов, но больше не поддерживается в современном стандарте */
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
