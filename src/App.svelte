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
    lists[index] = value;
  }
  function handleDelete(index: number) {
    lists.splice(index, 1);
    lists = lists;
  }
</script>

<div class="box">
  <Edit onAdd={handleAdd} />
  <List {lists} onEdit={handleEdit} onDelete={handleDelete} />
</div>
<footer>
  source :
  <a
    href="https://github.com/geekris1/svelte-todolist"
    target="_blank"
    rel="noreferrer"
  >
    https://github.com/geekris1/svelte-todolist</a
  >
</footer>

<style lang="scss">
  .box {
    width: 50vw;
    height: 70vh;
    background-color: #333;
    border-radius: 8px;
    padding: 20px 30px;
  }
  @media (max-width: 1400px) {
    .box {
      width: 55vw;
      height: 75vh;
      background-color: #333;
      border-radius: 8px;
      padding: 20px 30px;
    }
  }

  @media (max-width: 1000px) {
    .box {
      width: 75vw;
      height: 80vh;
      background-color: #333;
      border-radius: 8px;
      padding: 20px 30px;
    }
  }

  footer {
    margin-top: 10px;
    a {
      color: #fff;
      &:link,
      &:hover,
      &:visited {
        color: #fff;
      }
    }
  }
</style>
