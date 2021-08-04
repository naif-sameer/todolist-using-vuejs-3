<template>
  <div>
    <NewItem class="rounded-top rounded-bottom" @addNewItem="addNewItem" />
    <ListControl
      @control:all="filterControlAll"
      @control:active="filterControlActive"
      @control:complete="filterControlcomplete"
      :btnActive="btnActive"
      :list-length="listLength"
    />
    <div
      v-show="listItems.length > 0"
      class="list-items shadow-md mt-1 mx-center rounded-top rounded-bottom"
    >
      <template v-for="item in listItems" :key="item.id">
        <div class="list__item px-10" v-show="item.isShow">
          <!-- complete btn -->
          <div
            @click="completeItem(item.id)"
            class="list__complete-btn cursor-pointer"
          >
            <svg
              class="btn__icon"
              :class="item.iscomplete ? '' : 'd-none'"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 425.39996337890625 395.1000061035156"
            >
              <path
                d="M404.2 13.4c-17.3-13.4-41.5-9.3-54.1 9.1L170.2 285.7 71.1 178.4C56.5 161.8 32 161 16.4 176.6.8 192.1 0 218.2 14.7 234.7c0 0 120.4 133.6 137.7 147 17.3 13.4 41.5 9.3 54.1-9.1L412.8 70.9c12.6-18.5 8.7-44.2-8.6-57.5z"
              />
            </svg>
          </div>

          <!-- edite todo list -->
          <EditInput
            v-model:content="item.content"
            v-model:is-edit="item.isEdit"
            v-if="item.isEdit"
          />

          <template v-else>
            <!-- item content -->
            <div
              :class="{ 'complete__item-done': item.iscomplete }"
              class="list__content"
              v-text="item.content"
              @dblclick="item.isEdit = true"
            ></div>

            <!-- delete btn -->
            <button
              :data-item-id="item.id"
              class="list__delete-btn cursor-pointer"
              @click="deleteItem(item.id)"
            >
              X
            </button>
          </template>
        </div>
      </template>
    </div>
  </div>
</template>

<script>
import NewItem from "./NewItem.vue";
import ListControl from "./ListControl.vue";
import EditInput from "./EditInput.vue";

export default {
  name: "ListItem",
  components: {
    NewItem,
    ListControl,
    EditInput,
  },
  data() {
    return {
      listItems: [
        {
          id: 1000000,
          content: "code by naif4web",
          iscomplete: false,
          isShow: true,
          isEdit: false,
        },
      ],
      btnActive: "",
    };
  },
  methods: {
    addNewItem(newItem) {
      // insert new item in listItems
      this.listItems = [...this.listItems, { ...newItem }];
    },
    completeItem(id) {
      this.listItems.map((item) => {
        if (item.id === id) {
          return (item.iscomplete = !item.iscomplete);
        }
        return item;
      });
    },
    deleteItem(id) {
      // delete item using filter
      this.listItems = this.listItems.filter((item) => item.id !== id);
    },
    filterControlAll() {
      this.btnActive = "all";
      this.listItems = this.listItems.map((item) => {
        return { ...item, isShow: true };
      });
    },
    filterControlActive() {
      this.btnActive = "active";
      this.listItems = this.listItems.map((item) => {
        return {
          ...item,
          isShow: !item.iscomplete,
        };
      });
    },
    filterControlcomplete() {
      this.btnActive = "complete";
      this.listItems = this.listItems.map((item) => {
        return {
          ...item,
          isShow: item.iscomplete,
        };
      });
    },
  },

  computed: {
    listLength() {
      // only count { isShow: true } items
      return this.listItems.filter((item) => item.isShow).length;
    },
  },
};
</script>

<style scoped lang="scss">
.complete__item-done {
  text-decoration: line-through;
  color: var(--item-done-color);
}

.list-items {
  background-color: var(--primary-color);
  overflow: hidden;
}

.list__item {
  --p: 0.8em;
  display: flex;
  padding-bottom: var(--p);
  padding-top: var(--p);
  position: relative;
  border-bottom: 1px solid var(--third-color);
  overflow: hidden;

  .list__complete-btn {
    $size: 30px;
    width: $size;
    height: $size;
    background: var(--third-color);
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;

    .btn__icon {
      width: ($size / 2);
      height: ($size / 2);
      fill: green;
    }
  }

  .list__content {
    padding-left: 0.8em;
    display: flex;
    align-items: center;
    max-width: 80%;
    word-break: break-all;
    overflow: hidden;
  }
}

.list__delete-btn {
  background-color: var(--btn-bg-color);
  height: 100%;
  padding: 0.8em 1em;
  font-size: 1.3rem;
  position: absolute;
  top: 0;
  right: 0;
  border: none;
  color: #9ca3af;
  transition: background-color 0.2s ease;
}

.list__item .list__delete-btn:hover {
  background-color: var(--btn-bg-darken-color);
}
</style>