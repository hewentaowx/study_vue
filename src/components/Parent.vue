/* eslint-disable vue/return-in-computed-property */
<template>
  <div class="parent">
    <h1>{{ msg }}</h1>
    <button class="btn" @click="getNum">{{num}}</button>
    <ul>
        <li v-for="(movie,index) in movies" :key="movie"
        :class="{active: currentIndex === index}"
        @click="isClick(index)">
        {{movie}}
        </li>
    </ul>
    <table>
      <thead>
        <tr>
          <th>语文</th>
          <th>数学</th>
          <th>外语</th>
          <th>物理</th>
          <th>化学</th>
          <th>生物</th>
          <th>总分</th>
        </tr>
      </thead>
      <tbody>
      <tr>
        <td v-for="(item, index) in subjects" :key="index">{{item.value}}</td>
        <td>{{getTotalSum()}}</td>
      </tr>
      </tbody>
    </table>
    <div v-if="this.books.length > 0">
      <table>
        <thead>
          <th></th>
          <th>书籍名称</th>
          <th>出版时间</th>
          <th>价格</th>
          <th>数量</th>
          <th>操作</th>
        </thead>
        <tbody>
          <tr v-for="(book, index) in books" :key="index">
            <td>{{book.id}}</td>
            <td>{{book.bookName}}</td>
            <td>{{book.time}}</td>
            <td>{{book.price | showPrice }}</td>
            <td>
              <button @click="decrement(index)" :disabled="book.count <= 1">-</button>
              {{book.count}}
              <button @click="increment(index)">+</button>
            </td>
            <td>
              <button @click="removeItem(index)">移除</button>
            </td>
          </tr>
        </tbody>
      </table>
      <h2>总价格：{{totalPrice | showPrice }}</h2>
    </div>
    <div v-else>
      <h2>暂无数据</h2>
    </div>

    <children title="hhhhh" date="2020-12-21">
    <div>
    </div>
  </children>
  </div>

</template>

<script>
import Children from '@/components/Children'

export default {
  name: 'Parent',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      num: 0,
      movies: ['星际穿越', '阿凡达', '八佰', '金刚川', '黑鹰坠落'],
      currentIndex: 0,
      totalSum: 0,
      subjects: [
        { id: 1, key: '语文', value: 130 },
        { id: 2, key: '数学', value: 150 },
        { id: 3, key: '外语', value: 140 },
        { id: 4, key: '物理', value: 80 },
        { id: 5, key: '化学', value: 90 },
        { id: 6, key: '生物', value: 70 }
      ],
      books: [
        { id: 1, bookName: 'JavaScript开发手册', time: '2020-12-09', price: 50, count: 1 },
        { id: 2, bookName: '代码整洁之道', time: '2020-09-01', price: 60, count: 1 },
        { id: 3, bookName: '犀牛书', time: '2020-12-08', price: 70, count: 1 },
        { id: 4, bookName: 'JavaScript高程', time: '2020-02-10', price: 80, count: 1 },
        { id: 5, bookName: 'Java编程思想', time: '2020-11-11', price: 90, count: 1 }
      ]
    }
  },
  filters: {
    showPrice (price) {
      return `￥${price.toFixed(2)}`
    }
  },
  methods: {
    getNum () {
      this.num++
    },
    isClick (index) {
      this.currentIndex = index
    },
    getTotalSum () {
      // eslint-disable-next-line no-return-assign
      return this.subjects.reduce((a, c) => a += c.value, 0)
    },
    decrement (index) {
      this.books[index].count--
    },
    increment (index) {
      this.books[index].count++
    },
    removeItem (index) {
      this.books.splice(index, 1)
    }
  },
  computed: {
    // 你好kkkkkk
    // eslint-disable-next-line vue/return-in-computed-property
    totalPrice () {
      // eslint-disable-next-line no-return-assign
      let allPrice = this.books.reduce((a, c) => a += (c.price * c.count), 0)
      return allPrice
    }
  },
  components: {
    Children
  }
}
</script>

<style scoped>
.active {
  color: #42b983;
}
.btn {
  width: 80px;
}
h1, h2, table {
  font-weight: normal;
}
ul, table {
  list-style-type: none;
  padding: 0;
}
li, table{
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

table {
  border: 1px solid #e9e9e9;
  border-collapse: collapse;
  border-spacing: 0;
}

th, td {
  padding: 8px 16px;
  border: 1px solid #e9e9e9;
  text-align: left;
}

th {
  background-color: #f7f7f7;
  color: #5c6d77;
  font-weight: 600;
  text-align: center;
}
</style>
