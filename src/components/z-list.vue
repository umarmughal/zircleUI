<template>
  
 <section title="z-list">
   <z-item 
    :color="color"
    size="small"
    :distance="60"
    v-for="(item, index) in items"
    :key="index"
    :total="items.length"
    :index="index"
    layout='radial'
    gotoview="item"
    :item="item">
      {{item}}
    </z-item>
    <z-pagination  
    :collect="resdata"
    :per-page="perPage"
    @updateItems="displayedItems" />
</section>
</template>

<script>
import zmixin from '../mixins/zircle-mixin'
export default {
  name: 'z-list',
  mixins: [zmixin],
  props: {
    collection: {
      type: Array
    },
    perPage: {
      type: [Number]
    }
  },
  data () {
    return {
      items: [],
      type: 'panel', // esto es para evitar que se compute mal position y escala,
      resdata: this.collection
    }
  },
  methods: {
    displayedItems (data) {
      this.items = data.data
      this.$emit('updateProgress', data.progress)
    }
  }
}
</script>