<script setup>

</script>

<template>
  <main class=" pt-10 pl-10">
    <div class="add w-full gap-[20px] flex mb-5">
      <input type="text" value=" 改建案" id="" class="add-text border-2 border-black">
      <button class="add-Todo text-white bg-blue-500  py-1 px-4" type="button">新增</button>
    </div>

    <div class="search-btn mb-5">
      <button class="all text-white bg-blue-500  py-1 px-4 mr-2" type="button">全部</button>
      <button class="is-todo  text-white bg-blue-500  py-1 px-4 mr-2" type="button">已執行</button>
      <button class="not-todo  text-white bg-blue-500  py-1 px-4 mr-2" type="button">未執行</button>
    </div>

    <table class="todo w-full text-center  border-collapse table-auto">
      <thead>
        <tr>
          <th>執行</th>
          <th>事項</th>
          <th>功能</th>
        </tr>
      </thead>
      <tbody class="data-show">
        <tr>
          <td>
            <input type="checkbox">
          </td>
          <td></td>
          <td>
            <button type="button" class="text-white bg-blue-500  py-1 px-4 mr-3 ">編輯</button>
            <button type="button" class="text-white bg-blue-500  py-1 px-4  ">刪除</button>
          </td>
        </tr>
      </tbody>
    </table>
  </main>
</template>
<style>

th,td {
  border-bottom: 1px solid black;
}
</style>