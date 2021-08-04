<template>
  <div class="new-item mx-center shadow-md">
    <input
      class="new-item__input"
      type="text"
      placeholder="Add new item"
      v-model="item.content"
      @keyup.enter="addNewItem"
    />
    <button class="new-item__btn cursor-pointer" @click="addNewItem">
      Add
    </button>
  </div>
</template>

<script>
export default {
  name: "NewItem",
  data() {
    return {
      item: {
        content: "",
        id: 0,
        iscomplete: false,
        isShow: true,
        isEdit: false,
      },
    };
  },

  emits: ["addNewItem"],

  methods: {
    addNewItem() {
      if (this.item.content !== "") {
        this.$emit("addNewItem", this.item);
        this.item.content = "";
        this.item.id++;
      } else {
        console.log("please add some stuff here");
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.new-item {
  --border-radius: 8px;
  display: flex;

  &__input {
    font-size: 1rem;
    flex-basis: 90%;
    padding: 1.55em 1.2em;
    background-color: var(--primary-color);
    border: none;
    border-top-left-radius: var(--border-radius);
    border-bottom-left-radius: var(--border-radius);

    &:focus {
      outline: none;
      box-shadow: 0 0 0 20px var(--foucs-border);
    }
  }

  &__btn {
    font-size: 1rem;
    flex-basis: 10%;
    background-color: var(--btn-bg-color);
    padding: 1em 1.2em;
    color: #9ca3af;
    border: none;
    border-left: 2px solid var(--primary-color);
    border-top-right-radius: var(--border-radius);
    border-bottom-right-radius: var(--border-radius);
    transition: background-color 0.2s ease;

    &:hover {
      background-color: var(--btn-bg-darken-color);
    }
  }
}
</style>
