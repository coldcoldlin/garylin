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

  methods: {
    addEventData() {
      let message = this.inputValue;
      // let checkData = this.checkboxValue;
      if (!message) {
        alert('請重新輸入');
        return
      }
      const addArr = {
        eventId: this.id++,
        text: message,
        checkStatus: false,
      }
      this.arr.push(addArr);
    },
    eventDataDelete(eventId) {
      // console.log(eventId);
      if (confirm('是否要刪除') == true) {
        this.arr = this.arr.filter((item) => item.eventId !== eventId)
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
    },
  },

  computed: {
    filterArrdata() {
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
      <button class="is-todo  text-white bg-blue-500  py-1 px-4 mr-2" type="button"
        :class="{ 'active': selectedTab === true }" @click="changeTab(true)">已執行</button>
      <button class="not-todo  text-white bg-blue-500  py-1 px-4 mr-2" type="button"
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
      <tbody v-for="(item, index) in filterArrdata" :key="index" class="data-show">
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
};
;</style>