<script>
export default {
  name: "TableRowCategory",
  props: ["categories"],
};
</script>

<template>
  <tr>
    <td class="p-3 text-xs">{{ categories.id }}</td>
    <td class="p-3 text-xs">{{ categories.name }}</td>
  </tr>
</template>
