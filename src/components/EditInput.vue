<template>
  <input
    type="text"
    class="edit-list__input py-10 px-10"
    :value="content"
    @keyup.enter="
      $emit('update:isEdit', false),
        $emit('update:content', $event.target.value)
    "
    @blur="
      $emit('update:isEdit', false),
        $emit('update:content', $event.target.value)
    "
  />
</template>

<script>
export default {
  name: "EditInput",
  props: {
    content: String,
    isEdit: Boolean,
  },
  emits: ["update:content", "update:isEdit"],

  mounted() {
    this.$nextTick(function (...el) {
      // focus on input
      this.$el.focus()
    });
  },
};
</script>

<style lang="scss" scoped>
.edit-list__input {
  --py: 1.2em;
  width: 90%;
  margin-left: 0.8em;
  position: absolute;
  top: 50%;
  left: 2.8em;
  transform: translateY(-50%);
  font-size: 1rem;
  border: 1px solid var(--btn-bg-darken-color);
  background-color: var(--btn-bg-darken-color);

  &:focus {
    outline: none;
  }
}
</style>