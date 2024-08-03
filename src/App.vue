<script setup>
import { ref } from 'vue'

const data = [
  {
    id: 1,
    title: '珍珠奶茶',
    description: '香濃奶茶搭配QQ珍珠',
    price: 50,
    stock: 20
  },
  {
    id: 2,
    title: '冬瓜檸檬',
    description: '清新冬瓜配上新鮮檸檬',
    price: 45,
    stock: 18
  },
  {
    id: 3,
    title: '翡翠檸檬',
    description: '綠茶與檸檬的完美結合',
    price: 55,
    stock: 34
  },
  {
    id: 4,
    title: '四季春茶',
    description: '香醇四季春茶，回甘無比',
    price: 45,
    stock: 10
  },
  {
    id: 5,
    title: '阿薩姆奶茶',
    description: '阿薩姆紅茶搭配香醇鮮奶',
    price: 50,
    stock: 25
  },
  {
    id: 6,
    title: '檸檬冰茶',
    description: '檸檬與冰茶的清新組合',
    price: 45,
    stock: 20
  },
  {
    id: 7,
    title: '芒果綠茶',
    description: '芒果與綠茶的獨特風味',
    price: 55,
    stock: 18
  },
  {
    id: 8,
    title: '抹茶拿鐵',
    description: '抹茶與鮮奶的絕配',
    price: 60,
    stock: 20
  }
]

const drinks = ref(data)

const tempEdit = ref({
  id: '',
  title: '',
  description: '',
  price: '',
  stock: ''
})

const updateStock = (id, newStock) => {
  drinks.value = drinks.value.map((item) => {
    if (item.id === id) {
      item.stock = newStock
    }
    return item
  })
}

const prepareEdit = (item) => {
  tempEdit.value = { ...item }
  console.log(tempEdit.value)
}

const confirmEdit = () => {
  const index = drinks.value.findIndex((item) => item.id === tempEdit.value.id)
  drinks.value[index] = tempEdit.value
  tempEdit.value = {}
}
</script>

<template>
  <div class="table mt-5 text-center">
    <h1>第一週作業</h1>
    <table class="table mt-5">
      <thead class="table-info">
        <tr>
          <th scope="col">品項</th>
          <th scope="col">描述</th>
          <th scope="col">價格</th>
          <th scope="col">庫存</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in drinks" :key="item.id">
          <td>
            <div v-if="tempEdit.id !== item.id">
              {{ item.title }}
              <button type="button" class="btn btn-info ms-3" @click="prepareEdit(item)">編輯</button>
            </div>
            <div v-else>
              <input type="text" v-model="tempEdit.title" />
              <button type="button" class="btn btn-info" @click="confirmEdit">修改</button>
              <button type="button" class="btn btn-outline-secondary" @click="tempEdit = {}">
                取消
              </button>
            </div>
          </td>
          <td>
            <small>{{ item.description }}</small>
          </td>
          <td>{{ item.price }}</td>
          <td>
            <button
              type="button"
              class="btn btn-info"
              @click="updateStock(item.id, item.stock - 1)"
              :disabled="item.stock < 1"
            >
              -
            </button>
            {{ item.stock }}
            <button
              type="button"
              class="btn btn-info"
              @click="updateStock(item.id, item.stock + 1)"
            >
              +
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style scoped>
.table {
  max-width: 1200px;
  margin: 0 auto;
}
</style>
