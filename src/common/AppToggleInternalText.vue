<template>
  <label
    class="container"
    :style="'--switch-container-width: 20rem'"
    @click="update"
  >
    <input
      v-bind="$attrs"
      class="input"
      type="checkbox"
      :checked="checked"
      @change="$emit('update:checked', $event.target.checked)"
    />
    <span class="switch"></span>
    <span :class="{ leftEnabled: !checked, leftDisabled: checked }">{{
      leftText
    }}</span>
    <span :class="{ rightDisabled: !checked, rightEnabled: checked }">{{
      rightText
    }}</span>
  </label>
</template>

<script>
export default {
  name: "Switch",
  props: {
    leftText: {
      type: String,
      required: true
    },
    rightText: {
      type: String,
      required: true
    },
    checked: {
      type: Boolean,
      required: true
    }
  },
  emits: ["update:checked", "update"],
  methods: {
    update() {
      this.$emit("update");
    }
  }
};
</script>

<style scoped>
.container {
  width: var(--switch-container-width);
  cursor: pointer;
  display: flex;
  align-items: center;
}
.leftDisabled {
  flex-shrink: 0;
  margin-left: calc(var(--switch-container-width) * -1 + 2rem);
  color: #c4c4c4;
}
.leftEnabled {
  flex-shrink: 0;
  margin-left: calc(var(--switch-container-width) * -1 + 2rem);
  color: #020f22;
}
.rightDisabled {
  flex-shrink: 0;
  margin-left: 3rem;
  color: #c4c4c4;
}
.rightEnabled {
  flex-shrink: 0;
  margin-left: 3rem;
  color: #020f22;
}
/* Visually hide the checkbox input */
.input {
  /* position: relative; */
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border-width: 0;
}
.switch {
  --switch-container-size: 80px;
  --switch-size: calc(var(--switch-container-size) / 2);
  --blue: #4760f3;
  --dark-blue: #3a4fca;
  --white: #fff;
  --accent: #375786;
  /* Vertically center the inner circle */
  display: flex;
  align-items: center;
  position: relative;
  height: var(--switch-size);
  flex-basis: var(--switch-container-width);
  z-index: -1;
  /* Make the container element rounded */
  border-radius: var(--switch-size);
  background-color: white;
  /* In case the label gets really long, the toggle shouldn't shrink. */
  flex-shrink: 0;
  border: 2px solid var(--accent);
  transition: background-color 0.25s ease-in-out;
}
.switch::before {
  content: "";
  /* position: absolute; */
  height: calc(var(--switch-size) - 4px);
  width: calc(var(--switch-container-width) / 2);
  /* Make the inner circle fully rounded */
  border-radius: var(--switch-size);
  background-color: var(--white);
  border: 2px solid var(--accent);
  transition: transform 0.375s ease-in-out;
}
.input:checked + .switch::before {
  /* Move the inner circle to the right */
  transform: translateX(calc(var(--switch-container-width) / 2));
}
</style>
