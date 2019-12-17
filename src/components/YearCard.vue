<template>
  <li class="md:table-row py-4">
    <span class="md:table-cell text-md whitespace-no-wrap px-3">{{years}}</span>
    <div class="md:table-cell px-3 py-2 whitespace-normal text-md" :class="{ 'text-xl': edge.current }">
      <slot />
    </div>
  </li>
</template>

<script>
export default {
  props: ['edge', 'years'],
  name: 'YearCard',
}
</script>