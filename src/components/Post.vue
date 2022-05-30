<template>
  <article>
    <h2>{{ title }}</h2>
    <p>{{ content }}</p>
    <p>
      {{ firstname }}{{ lastname }} on
      {{ new Date(date).toLocaleDateString() }}
    </p>
  </article>
</template>

<script>
export default {
  props: {
    title: String,
    content: String,
    firstname: String,
    lastname: String,
    date: String,
  },
};
</script>
