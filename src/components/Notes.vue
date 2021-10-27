<template>
  <!--note list-->
  <div class="notes">
    <!-- если !grid в состоянии false, то появляется класс full -->
    <div
      class="note"
      :class="{ full: !grid }"
      v-for="(elem, index) in notes"
      :key="index"
    >
      <div :class="elem.selectPriotity">
        <div class="note-header" :class="{ full: !grid }">
          <h3>{{ elem.title }}</h3>
          <p
            style="cursor: pointer; color: #402caf; font-weight: 800"
            @click="removeNote(index)"
          >
            x
          </p>
        </div>
        <div class="note-body">
          <p>{{ elem.descr }}</p>
          <span>{{ elem.date }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    notes: {
      type: Array,
      required: true,
    },
    grid: {
      type: Boolean,
      required: true,
    },
  },
  methods: {
    removeNote(index) {
      //новый метод, для удаления заметки
      this.$emit("remove", index);
    },
  },
};
</script>

<style lang="scss">
.notes {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  padding: 30px 0;
}
.note {
  width: 48%;
  margin-bottom: 20px;
  background-color: #fff;
  transition: all 0.25s cubic-bezier(0.02, 0.01, 0.47, 1);
  box-shadow: 0 30px 30px rgba(0, 0, 0, 0.2);
  &:hover {
    box-shadow: 0 30px 30px rgba(0, 0, 0, 0.4);
    transform: translateY(-6px);
    // transition-delay: 0s !important ;
  }
  &.full {
    width: 100%;
    text-align: center;
  }

  .low-priority {
    width: 100%;
    background-color: rgb(240, 240, 170);
    padding: 20px;
    word-wrap: break-word;
    overflow: auto;
  }

  .high-priority {
    width: 100%;
    background-color: rgba(243, 93, 93, 0.712);
    padding: 20px;
    word-wrap: break-word;
    overflow: auto;
  }

  .default-priority {
    width: 100%;
    padding: 20px;
    word-wrap: break-word;
    overflow: auto;
  }
}
.note-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  h1 {
    font-size: 32px;
  }
  h3 {
    font-size: 22px;
    color: #402caf;
  }
  svg {
    margin-right: 12px;
    color: #999;
    &.active {
      color: #402caf;
    }
    &:last-child {
      margin-right: 0;
    }
  }
  &.full {
    justify-content: center;
    h3 {
      margin-right: 16px;
      &:last-child {
        margin-right: 0;
      }
    }
  }
}
.note-body {
  p {
    margin: 20px 0;
  }
  span {
    font-size: 14px;
    color: #999;
  }
}
</style>