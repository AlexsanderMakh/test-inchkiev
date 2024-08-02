<template>
  <div>
    <label>
      <input type="radio" name="sort" value="alphabetical" :checked="selectedSort === 'alphabetical'" @change="$emit('update:selectedSort', 'alphabetical')">
      Відсортувати блоки за заголовком відповідно до алфавітного порядку
    </label>
    <label>
      <input type="radio" name="sort" value="imageLeft" :checked="selectedSort === 'imageLeft'" @change="$emit('update:selectedSort', 'imageLeft')">
      Вивести всі блоки у форматі "зображення - зліва, текст - справа"
    </label>
    <label>
      <input type="radio" name="sort" value="alternating" :checked="selectedSort === 'alternating'" @change="$emit('update:selectedSort', 'alternating')">
      Вивести всі блоки у форматі "зображення - зліва, текст - справа" і навпаки в шаховому порядку
    </label>
  </div>
</template>

<script>
export default {
  props: {
    selectedSort: {
      type: String,
      required: true
    }
  }
}
</script>

<style scoped>
div {
  margin-bottom: 20px;
}

label {
  display: block;
  margin-bottom: 10px;
}
</style>
