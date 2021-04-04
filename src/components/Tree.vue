<template>
  <div class="tree" id="tree">
    <ul class="tree__list">
      <TreeItem
        :item="treeData"
        @make-folder="makeFolder"
        @add-item="addItem"
      />
    </ul>

    <div class="tree__out">
      <button v-on:click="showJson" class="tree__out-btn">
        Create
        <img
          class="tree__out-btn-img"
          src="../assets/JsonFormat.svg"
          alt="Json"
        />
      </button>
      <div class="tree__out-json" v-if="jsonIsShown">
        <pre><code>{{treeData}}</code></pre>
      </div>
    </div>
  </div>
</template>

<script>
import TreeItem from "@/components/TreeItem.vue";

export default {
  components: {
    TreeItem,
  },
  data() {
    return {
      treeData: {
        name: "Дерево записей",
        children: [
          { name: "Важная запись" },
          { name: "Заметка" },
          {
            name: "Список записей",
            children: [
              { name: "Важная запись" },
              { name: "Заметка" },
              {
                name: "Список записей",
                children: [{ name: "Важная запись" }, { name: "Заметка" }],
              },
              {
                name: "Список записей",
                children: [{ name: "Важная запись" }, { name: "Заметка" }],
              },
            ],
          },
        ],
      },
      jsonIsShown: false,
    };
  },
  methods: {
    makeFolder: function (item) {
      this.$set(item, "children", []);
      this.addItem(item);
    },
    addItem: function (item) {
      let newNoteName = prompt("Добавить новую запись:");

      if (newNoteName) {
        item.children.push({
          name: newNoteName,
        });
      }
    },
    showJson: function () {
      this.jsonIsShown = !this.jsonIsShown;
    },
  },
};
</script>

<style>
.tree {
  max-width: 700px;
  margin: 0 auto;
  background-color: rgba(21, 21, 22, 0.863);
  border: 1px solid rgb(56, 52, 52);
  border-radius: 10px;
  padding: 20px 10px;
}

.tree__list {
  margin: 0 auto 30px auto;
  width: 600px;
  border: 1px solid rgb(255, 252, 252);
  border-radius: 10px;
  background-color: rgb(204, 204, 204);
  padding: 10px;
}

.tree__out {
  margin: 0 auto;
  border: 2px solid rgb(214 212 212 / 82%);
  border-radius: 10px;
  padding: 10px;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
}

.tree__out-btn {
  line-height: 50px;
  height: 50px;
  text-align: center;
  width: 250px;
  cursor: pointer;
  font-size: 24px;
  color: rgb(136, 133, 133);
  transition: all 0.5s;
  position: relative;

  display: flex;
  justify-content: space-evenly;
  align-items: center;
}

.tree__out-btn::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 1;
  background-color: rgba(255, 255, 255, 0.3);
  transition: all 0.3s;
}
.tree__out-btn:hover::before {
  opacity: 0;
  transform: scale(0.5, 0.5);
}
.tree__out-btn::after {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 1;
  opacity: 0;
  transition: all 0.3s;
  border: 1px solid rgba(255, 255, 255, 0.5);
  transform: scale(1.2, 1.2);
}
.tree__out-btn:hover::after {
  opacity: 1;
  transform: scale(1, 1);
}

.tree__out-btn-img {
  object-fit: cover;
  height: 75%;
  filter: invert(0.6);
}

.tree__out-json {
  width: 100%;
  padding: 20px;
  background-color: azure;
  border-radius: 10px;
  overflow: hidden;
  margin-top: 20px;
  font-size: 14px;
}
</style>
