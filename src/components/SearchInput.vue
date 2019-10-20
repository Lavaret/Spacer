<style lang="scss" scoped>

input {
  height: 35px;
  border: 0;
  margin-top: 50px;
  width: 250px;
  color: white;
  padding-bottom: 15px;
  text-align: center;
  font-size: 30px;
  font-weight: 300;
  border-bottom: 1px solid white;
  background: none;
  transition: box-shadow .5s ease-out;
}

input:focus {
  outline: none;
  box-shadow: 0 14px 20px -12px rgba(255, 255, 255, .45);
}

.dark {
  color: #1e3d4a;
  border-bottom-color: #1e3d4a;
}

.dark:focus {
  outline: none;
  box-shadow: 0 15px 13px -14px rgba(#1e3d4a, .3);
}

</style>

<template>

<input
  type="text"
  id="search"
  name="search"
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
