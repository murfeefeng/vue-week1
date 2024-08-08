<template>
  <h2>商品明細</h2>
  <table>
    <thead>
      <tr>
        <th scope="col">品項</th>
        <th scope="col">描述</th>
        <th scope="col">價格</th>
        <th scope="col">庫存</th>
        <th scope="col">修改</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="dd in drinks" :key="dd.id">
        <td>{{ dd.name }}</td>
        <td>
          <small>{{ dd.detail }}</small>
        </td>
        <td>{{ dd.price }}</td>
        <td>
          <button type="button" @click="changeQty(dd.id, dd.qty - 1)" :disabled="dd.qty < 1">
            -
          </button>
          <span>{{ dd.qty }}</span>
          <button type="button" @click="changeQty(dd.id, dd.qty + 1)">+</button>
        </td>
        <td>
          <button type="button" @click="changeDD(dd)">修改</button>
        </td>
      </tr>
    </tbody>
  </table>
  <div class="editBg" v-show="showEdit">
    <div class="editBox">
      <h2>修改商品</h2>
      <ul class="editArea">
        <li>
          <span>更新品項：</span><input type="text" v-model="newDD.name" /> <span>預覽：</span
          ><i>{{ newDD.name }}</i>
        </li>
        <li>
          <span>更新描述：</span><input type="text" v-model="newDD.detail" /> <span>預覽：</span
          ><i>{{ newDD.detail }}</i>
        </li>
        <li>
          <span>更新價格：</span><input type="text" v-model="newDD.price" /> <span>預覽：</span
          ><i>{{ newDD.price }}</i>
        </li>
      </ul>
      <div class="btn2">
        <button type="button" @click="saveDD">儲存</button>
        <button type="button" @click="cancelEdit">取消</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const data = [
  {
    id: 1,
    name: '珍珠奶茶',
    detail: '香濃奶茶搭配QQ珍珠',
    price: 50,
    qty: 5
  },
  {
    id: 2,
    name: '冬瓜檸檬',
    detail: '清新冬瓜配上新鮮檸檬',
    price: 45,
    qty: 18
  },
  {
    id: 3,
    name: '翡翠檸檬',
    detail: '綠茶與檸檬的完美結合',
    price: 55,
    qty: 34
  },
  {
    id: 4,
    name: '四季春茶',
    detail: '香醇四季春茶，回甘無比',
    price: 45,
    qty: 10
  },
  {
    id: 5,
    name: '阿薩姆奶茶',
    detail: '阿薩姆紅茶搭配香醇鮮奶',
    price: 50,
    qty: 25
  },
  {
    id: 6,
    name: '檸檬冰茶',
    detail: '檸檬與冰茶的清新組合',
    price: 45,
    qty: 20
  },
  {
    id: 7,
    name: '芒果綠茶',
    detail: '芒果與綠茶的獨特風味',
    price: 55,
    qty: 18
  },
  {
    id: 8,
    name: '抹茶拿鐵',
    detail: '抹茶與鮮奶的絕配',
    price: 60,
    qty: 20
  }
]

const drinks = ref(data)

const showEdit = ref(false)

const changeQty = (id, qty) => {
  if (qty >= 0) {
    drinks.value.find((item) => {
      if (item.id === id) {
        item.qty = qty
      }
    })
  }
}

//3.暫存物件
const newDD = ref({
  id: '',
  name: '',
  detail: '',
  price: ''
})

//點擊修改，複製一份物件
const changeDD = (dd) => {
  // console.log(index)
  //1.建暫存物件 newDD 在外面
  //2.複製dd物件到 newDD
  newDD.value = { ...dd }
  // console.log('新的物件', newDD)
  showEdit.value = true
}

const saveDD = () => {
  //找對應的index
  const index = drinks.value.findIndex((item) => item.id === newDD.value.id)
  console.log(index)
  //更新原有的array
  drinks.value[index] = newDD.value
  newDD.value = {}
  showEdit.value = false
}
const cancelEdit = () => {
  newDD.value = {}
  showEdit.value = false
}
</script>
