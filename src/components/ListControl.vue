<template>
  <div class="list-control rounded-top rounded-bottom">
    <button
      @click="$emit('control:all')"
      class="list-control__btn cursor-pointer"
      :class="{
        'btn-active': btnActive !== `complete` && btnActive !== `active`,
      }"
    >
      All
    </button>
    <button
      @click="$emit('control:active')"
      class="list-control__btn cursor-pointer"
      :class="{
        'btn-active': btnActive === `active`,
      }"
    >
      Active
    </button>
    <button
      @click="$emit('control:complete')"
      class="list-control__btn cursor-pointer"
      :class="{
        'btn-active': btnActive === `complete`,
      }"
    >
      complete
    </button>

    <div class="list-progress px-10">
      {{ listLength }} {{ listLength > 1 ? "items" : "item" }}
    </div>
  </div>
</template>

<script>
export default {
  emits: ["control:all", "control:active", "control:complete"],
  name: "ListControl",
  props: ["btnActive", "listLength"],
};
</script>

<style lang="scss" scoped>
.list-control {
  margin-top: 2em;
  background-color: var(--primary-color);
  overflow: hidden;
  position: relative;

  .list-control__btn {
    background-color: var(--btn-bg-color);
    border: none;
    font-size: 1.1rem;
    padding: 1em 1.2em;
    color: gray;
    transition: 0.3s ease;
    transition-property: background-color, color;

    &:hover {
      background-color: var(--btn-bg-darken-color);
    }

    &:not(:first-of-type) {
      border-left: 1px solid var(--third-color);
    }
  }

  .btn-active {
    color: var(--primary-text-color);
    background-color: var(--btn-bg-darken-color);
  }

  .list-progress {
    display: none;
    color: var(--secondary-text-color);
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    
    @media (min-width: 400px) {
      & {
        display: flex;
        align-items: center;
      }
    }
  }
}
</style>