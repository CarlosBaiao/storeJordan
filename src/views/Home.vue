<template>
  <div class="home">
    <SloganMenu/>
    <CategoryMenu/>
    <ItemsList/>
  </div>
</template>

<script>
import SloganMenu from '@/components/SloganMenu.vue'
import CategoryMenu from '@/components/CategoryMenu.vue'
import ItemsList from '@/components/ItemsList'




export default {
  name: 'Home',
  components: {
    CategoryMenu,
    SloganMenu,
    ItemsList,
  }
}

</script>
