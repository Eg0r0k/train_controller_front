<template>
  <div class="buffer">
    <div class="buffer__top">
      <div class="buffer__first_line">
        <p class="buffer__name">{{ inventory_name.split(':', 2)[1] }}</p>
      </div>
      <hr />
      <div class="buffer__item" v-for="item in inventory?.items" :key="item.item_name">
        {{ inventoryName }}
        {{ item.item_count }} / {{ item.max_stack * item.slots }}
      </div>
    </div>
    <p class="buffer__free">Free slots: {{ inventory?.max_slots - inventory?.used_slots }}</p>
  </div>
</template>

<script setup>
import { defineProps, computed } from 'vue'
import { useFactoryStore } from '@/app/store/factoryStore'

const factoryStore = useFactoryStore()

const inventory = computed(() => {
  return factoryStore.getFactory(bufferProps.factory_uuid)?.inventories[bufferProps.inventory_name]
})

const inventoryName = computed(() => bufferProps.inventory_name.split(':', 2)[1])

const bufferProps = defineProps({
  inventory_name: String,
  factory_uuid: String
})
</script>

<style lang="scss">
.buffer {
  background-color: rgb(34, 34, 34);
  border-radius: 10px;
  padding: 10px;
  gap: 10px;
  display: flex;
  flex-direction: column;
  width: max-content;
  justify-content: space-between;

  &__top {
    display: flex;
    flex-direction: column;
    gap: 10px;
  }

  &__first_line {
    gap: 10px;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
  }
}
</style>
