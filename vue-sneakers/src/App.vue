<script setup>
  import { onMounted, ref, watch, reactive } from 'vue'
  import axios from 'axios'
  import Header from './components/Header.vue'
  import CardList from './components/CardList.vue'
  import Drawer from './components/Drawer.vue'

  const items = ref([]);


const filters = reactive({
  sortBy: '',
  searchQuery: '',
});


  const onChangeSelect = event => {
    filters.sortBy = event.target.value
  }

  onMounted(async () => {
    try{
      const { data } = await axios.get("https://5e21e451e625add2.mokky.dev/items")

      items.value = data
    } catch (err){
      console.log(err)
    }
  });

  watch(filters, async () => {
    try{
      const { data } = await axios.get("https://5e21e451e625add2.mokky.dev/items?sortBy=" + filters.sortBy)

      items.value = data
    } catch (err){
      console.log(err)
    }
  });


</script>

<template>
<!--  <Drawer />-->
  <div class="bg-white w-4/5 m-auto rounded-xl shadow-xl mt-14">
    <Header />

    <div class="p-10">
      <div class="flex justify-between items-center">
        <h2 class="text-3xl font-bold mb-8">Все кроссовки</h2>

        <div class="flex gap-4">
          <select @change="onChangeSelect" class="py-2 px-3 border rounded-md outline-none">
            <option value="name">По названию</option>
            <option value="price">По цене(дешевые)</option>
            <option value="-price">По цене(дорогие)</option>
          </select>

          <div class="relative">
            <img class="absolute left-4 top-3" src="/search.svg" alt="search" />
            <input class="border rounded-md py-2 pl-11 pr-4 outline-none focus:border-gray-400 transition"
                   placeholder="Поиск"
            />
          </div>
        </div>
      </div>

      <div class="mt-10">
        <CardList :items="items" />
      </div>
    </div>
  </div>
</template>

