<template>
  <div>
    <input
      type="text"
      class="
        ease-in-out
        text-base
        bg-gray-100 bg-opacity-50
        rounded
        border border-gray-300
        focus:bg-white focus:ring-2
      "
      :value="value"
      @input="inputChange($event.target.value)"
      @keydown="handleNav"
      @focus="showOptions = true"
      @blur="onBlur"
    />
    <template v-if="showOptions">
      <template v-for="(filteredOption, index) in filteredOptions">
        <div
          :class="{ 'bg-gray-100': cursor === index }"
          class="hover:bg-gray-100 rounded-lg"
          :key="filteredOption + '_' + index"
          @mousedown="select(filteredOption)"
        >
          {{ filteredOption }}
        </div>
      </template>
    </template>
  </div>
</template>

<script>
export default {
  name: "AutoComplete",
  data() {
    return {
      options: ["option1", "option2", "option3"],
      cursor: -1,
      showOptions: false,
    }
  },
  props: {
    value: {
      type: String,
      default: "",
    },
  },
  methods: {
    moveCursorDown() {
      if (this.cursor < this.filteredOptions.length - 1) {
        this.cursor += 1
      }
    },
    moveCursorUp() {
      if (this.cursor > 0) {
        this.cursor -= 1
      }
    },
    select(text) {
      this.$emit("input", text)
      this.showOptions = false
    },
    inputChange(text) {
      this.$emit("input", text)
      this.cursor = -1
      if (!this.showOptions) {
        this.showOptions = true
      }
    },
    onBlur() {
      this.showOptions = false
    },
    handleNav(e) {
      switch (e.key) {
        case "ArrowUp":
          this.moveCursorUp()
          break
        case "ArrowDown":
          this.moveCursorDown()
          break
        case "Enter":
          if (this.cursor >= 0 && this.cursor < this.filteredOptions.length) {
            this.select(this.cursorItem)
          }
          break
      }
    },
  },
  computed: {
    filteredOptions() {
      return this.options.filter((option) => option.includes(this.value))
    },
    cursorItem() {
      return this.filteredOptions[this.cursor]
    },
  },
}
</script>
