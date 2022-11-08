<script lang="ts">
  import List from "./lib/List.svelte";
  import Edit from "./lib/Edit.svelte";
  let lists = [];
  function handleAdd(data) {
    // tip:没办法直接lists.push(data)
    // svelte的更新是由的!!!<赋值语句>触发
    // 所以可以
    // lists.push(data)
    // lists = lists
    // or
    // 我下面这个写法
    lists = [...lists, data];
  }
  function handleEdit(index: number, value: string) {
    console.log(index, value);
    lists[index] = value;
  }
  function handleDelete(index: number) {
    lists.splice(index, 1);
    lists = lists;
  }
</script>

<div class="box">
  <Edit {handleAdd} />
  <List {lists} onEdit={handleEdit} onDelete={handleDelete} />
</div>

<style lang="scss">
  .box {
    width: 40vw;
    height: 60vh;
    background-color: #333;
    border-radius: 8px;
  }
</style>
