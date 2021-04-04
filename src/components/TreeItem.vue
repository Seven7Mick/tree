<template>
  <li class="tree-item" v-show="item.name != null">
    <button
      :class="['tree-item__btn', btnArrowClass, { btn_folder: isFolder }]"
      v-on:click="toggleList"
    >
      {{ item.name }}
    </button>
    <div class="tree-item__event-btn">
      <button
        class="tree-item__event-btn-folder"
        title="Сделать папкой"
        v-if="!isFolder"
        v-on:mousedown="makeFolder(item)"
      ></button>
      <button
        class="tree-item__event-btn-add"
        title="Переименовать объект"
        v-on:mousedown="renameItem(item.name)"
      ></button>
      <button
        class="tree-item__event-btn-remove"
        title="Удалить объект"
        v-on:mousedown="removeItem(item)"
      ></button>
    </div>

    <div class="tree-item__body" v-if="isFolder" v-show="isOpen">
      <ul class="tree-item__list">
        <TreeItem
          class="tree-item__item"
          v-for="child in item.children"
          :key="child.id"
          :item="child"
          v-on:make-folder="$emit('make-folder', $event)"
          v-on:add-item="$emit('add-item', $event)"
        ></TreeItem>
      </ul>

      <button class="tree-item__add-btn" v-on:click="$emit('add-item', item)">
        +
      </button>
    </div>
  </li>
</template>

<script>
export default {
  name: "TreeItem",
  components: {},
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      isOpen: false,
    };
  },
  computed: {
    isFolder: function () {
      return this.item.children && this.item.children.length;
    },
    btnArrowClass: function () {
      return !this.isFolder
        ? ""
        : this.isFolder && this.isOpen
        ? "tree-item__btn_arrow_down"
        : "tree-item__btn_arrow_right";
    },
  },
  methods: {
    toggleList: function () {
      this.isOpen = !this.isOpen;
    },
    makeFolder: function () {
      this.$emit("make-folder", this.item);
      console.log(this.item);
      this.isOpen = true;
    },
    renameItem: function (name) {
      this.item.name = prompt("Изменить данную запись на:") || name;
    },
    removeItem: function (item) {
      item.name = undefined;
      item.children = undefined;
    },
  },
};
</script>

<style>
.btn_folder {
  font-weight: 600;
}

.tree-item__btn {
  border: none;
  background: none;
  cursor: pointer;
  margin-bottom: 5px;
  padding: 2px 5px;
  margin-right: 100px;
  font-size: 18px;
  max-width: 320px;
}

.tree-item__btn::after {
  content: "";
  font-weight: 600;
  font-size: 18px;
}

.tree-item__btn_arrow_right::after {
  content: url('../assets/FolderClose.svg');
}

.tree-item__btn_arrow_down::after {
  content: url('../assets/FolderOpen.svg');
}

.tree-item__btn_type_folder {
  font-weight: bold;
}

.tree-item__event-btn {
  display: none;
}

.tree-item__btn:focus + .tree-item__event-btn {
  display: inline-block;
}

.tree-item__event-btn-folder {
  height: 20px;
  width: 20px;
  margin-right: 25px;
  background-image: url("../assets/Folder.svg");
  background-repeat: no-repeat;
  background-position: center;
}

.tree-item__event-btn-add {
  margin-right: 25px;
  height: 20px;
  width: 20px;
  background-image: url("../assets/AddFile.svg");
  background-repeat: no-repeat;
  background-position: center;
}

.tree-item__event-btn-remove {
  height: 20px;
  width: 20px;
  background-image: url("../assets/Remove.svg");
  background-repeat: no-repeat;
  background-position: center;
}

.tree-item__event-btn-folder:hover,
.tree-item__event-btn-add:hover,
.tree-item__event-btn-remove:hover {
  transform: scale(1.2);
}

.tree-item__body {
  padding-left: 1em;
  line-height: 1.5em;
}

</style>
