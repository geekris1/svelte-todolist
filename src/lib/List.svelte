<script lang="ts">
  import { afterUpdate } from "svelte";
  import type { EditFunction, DeleteFunction, List } from "../types";
  export let onEdit: EditFunction;
  export let onDelete: DeleteFunction;
  export let lists: List = [];

  let editIndex;
  let inputValue;

  // 处理删除
  function handleDelete(index) {
    onDelete(index);
  }
  // 处理编辑
  // 一次只能修改一个
  function handleEdit(index, value) {
    editIndex = index;
    inputValue = value;
  }
  // 处理确认编辑
  function handleSureEdit(index) {
    if (inputValue === "") {
      return onDelete(index);
    }
    onEdit(index, inputValue);
    editIndex = undefined;
    inputValue = undefined;
  }
  // 处理取消编辑
  function handleCancel() {
    editIndex = undefined;
    inputValue = undefined;
  }
  // 处理编辑时input的输入
  function handleInputChange(e) {
    inputValue = e.target.value;
  }
</script>

<div class="container">
  {#each lists as list, index (index)}
    <div class="list">
      {#if index === editIndex}
        <input
          bind:value={inputValue}
          placeholder="请输入代办项。注意：如空值确认则会删除该项！"
          on:input={handleInputChange}
        />
      {:else}
        <span title={list}>{list}</span>
      {/if}

      <div class="event">
        {#if index === editIndex}
          <button
            on:click={() => {
              handleSureEdit(index);
            }}>确认</button
          >
          <button on:click={handleCancel}>取消</button>
        {:else}
          <button
            on:click={() => {
              handleEdit(index, list);
            }}>编辑</button
          >
          <button
            on:click={() => {
              onDelete(index);
            }}>删除</button
          >
        {/if}
      </div>
    </div>
  {:else}
    <div class="no-data">暂无代办项,请添加</div>
  {/each}
</div>

<style lang="scss">
  .container {
    height: calc(100% - 50px);
    overflow-x: auto;
    margin-top: 20px;
    &::-webkit-scrollbar {
      display: none;
    }
    .list {
      display: flex;
      align-items: center;
      justify-content: space-between;
      height: 45px;
      margin-bottom: 10px;
      .event {
        flex-basis: 125px;
      }
      input {
        width: calc(100% - 150px);
        height: 31px;
        font-size: 16px;
      }
      span {
        width: calc(100% - 150px);
        overflow: hidden;
        white-space: nowrap;
        text-overflow: ellipsis;
        text-align: left;
      }
    }
    .no-data {
      display: flex;
      align-items: center;
      justify-content: center;
      height: 100%;
    }
  }
</style>
