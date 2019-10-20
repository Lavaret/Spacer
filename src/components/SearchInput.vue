<template>
  <div class="search-input-wrapper">
    <input
     type="text"
     id="search"
     name="search"
     v-model="searchValue"
     @input="handleInput"
    />
  </div>
</div>
</template>

<script>
 export default {
   name: 'SearchInput'
 };

</script>

<style lang="scss" scoped>

  .search-input-wrapper {
    margin-top: 50px;
    display: flex;
    flex-direction: column;
    width: 250px;
  }

  input {
    height: 30px;
    border: 0;
    border-bottom: 1px solid black;
    background: none;
  }

</style>
