<script>
export default {
  data() {
    return {
      arr: [],
      inputValue: '',
      id: '',
      selectedTab: '',
      checkStatus: false,
    }
  },
  
  mounted(){

    if (localStorage.getItem('msg')) {
      this.arr = JSON.parse(localStorage.getItem('msg'));
    }
  },

  methods: {
    addEventData() {
      let message = this.inputValue;
      let id = this.arr.length ??0;
      // let checkData = this.checkboxValue;
      if (!message) {
        alert('請重新輸入');
        return
      }
      const addArr = {
        eventId: id + 1,
        text: message,
        checkStatus: false,
      }
      this.arr.push(addArr);
      console.log(this.arr);
      this.text = '';
      localStorage.setItem('msg', JSON.stringify(this.arr));
    },
    eventDataDelete(i) {
      // console.log(eventId);
      if (confirm('是否要刪除') == true) {
        this.arr = this.arr.filter((item) => item.eventId !== i)
        // this.arr.splice(i,1);
        localStorage.setItem('msg', JSON.stringify(this.arr));
      }
    },

    changeTab(tab) {
      this.selectedTab = tab;
    },

    textEditor(eventId) {
      this.arr.map((item) => {
        if (item.eventId == eventId) {
          let newMessage = prompt('修改文字');
          if (newMessage != '' || newMessage == null) {
            item.text = newMessage;
          }
        }
      })
      localStorage.setItem('msg', JSON.stringify(this.arr));
    },
  },
//預處理妳拿到的資料，他有暫存的功能，所以我們可以拿整包的資料，利用判斷式把我們的資料做篩選
  computed: {
    filterArrData() {
      if (this.selectedTab === '') {
        return this.arr;
      }
      return this.arr.filter(item => item.checkStatus === this.selectedTab);
    },
  }

}

</script>

<template>
  <main class=" pt-10 pl-10">
    <div class="add w-full gap-[20px] flex mb-5">
      <input v-model="inputValue" type="text" value="123" id="" class="add-text border-2 border-black">
      <button class="add-Todo text-white bg-blue-500  py-1 px-4 " type="button" @click="addEventData()">新增</button>
    </div>

    <div class="search-btn mb-5">
      <button class="all text-white bg-blue-500  py-1 px-4 mr-2 " type="button" :class="{ 'active': selectedTab === '' }"
        @click="changeTab('')">全部</button>
      <button class=" text-white bg-blue-500  py-1 px-4 mr-2" type="button"
        :class="{ 'active': selectedTab === true }" @click="changeTab(true)">已執行</button>
      <button class=" text-white bg-blue-500  py-1 px-4 mr-2" type="button"
        :class="{ 'active': selectedTab === false }" @click="changeTab(false)">未執行</button>
    </div>

    <table class="todo w-full text-center  border-collapse table-auto">
      <thead>
        <tr>
          <th>執行</th>
          <th>事項</th>
          <th>功能</th>
        </tr>
      </thead>
      <tbody v-for="(item, index) in filterArrData" :key="item.eventId" class="data-show">
        <tr>
          <td>
            <input v-model="item.checkStatus" type="checkbox">
          </td>
          <td>{{ item.text }}</td>
          <td>
            <button type="button" class="text-white bg-blue-500  py-1 px-4 mr-3 "
              @click="textEditor(item.eventId)">編輯</button>
            <button type="button" class="text-white bg-blue-500  py-1 px-4 "
              @click="eventDataDelete(item.eventId)">刪除</button>
          </td>
        </tr>
      </tbody>
    </table>
  </main>
</template>
<style scoped>
th,td {
  border-bottom: 1px solid black;
}
.active{
  @apply bg-yellow-500 text-black;
}
</style>