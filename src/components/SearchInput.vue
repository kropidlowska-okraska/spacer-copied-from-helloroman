<template>
    <input
      type="text"
      name="search"
      id="search"
      :class="{ dark }"
      :value="value"
      @input="handleChange"
    />
</template>

<script>
export default {
  name: 'SearchInput',
  props: {
    value: {
      type: String,
      required: true,
    },
    dark: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    handleChange(e) {
      this.$emit('input', e.target.value);
    },
  },
};
</script>

<style lang="scss" scoped>
  input {
    margin-top: 90px;
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 250px;
    height: 30px;
    border: 0;
    border-bottom: 1px solid white;
    background: none;
    color: white;
    font-size: 22px;
    font-family: 'Varela Round', sans-serif;
    text-align: center;
    outline: none;
    transition: box-shadow .5s;

    &:focus {
      outline: none;
      box-shadow: 0 10px 20px -8px rgba(255, 255, 255, 0.3);
    }
  }

  .dark {
    color: darkblue;
    border-bottom-color: darkblue;

    &:focus {
      outline: none;
      box-shadow: 0 10px 20px -8px rgba(darkblue, 0.3);
    }
  }
</style>
