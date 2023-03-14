<template>
  <nav class="breadcrumb">
    <ol>
      <li v-for="(item, index) in items" :key="index">
        <a :href="item.link">{{ item.text }}</a>
      </li>
    </ol>
  </nav>
</template>
<script>
export default {
  name: 'Breadcrumb',
  props: {
    items: {
      type: Array,
      required:true
    }
  }
}
</script>
<style>
.breadcrumb {
  background-color: white;
  font-size: 16px;
  padding: 2% 5%;
}

.breadcrumb ol {
  list-style: none;
  margin: 0;
  padding: 0;
  display: flex;
}

.breadcrumb li:not(:last-child)::after {
  content: '/';
  margin: 0 10px;
  color: black;
  text-decoration: none;
}

.breadcrumb li:not(last-child) a {
  color: #007A8D;
  text-decoration: none;
  font-weight: bold;
}

.breadcrumb li:last-child a {
  color: #666;
  pointer-events: none;
  text-decoration: none;
}
</style>