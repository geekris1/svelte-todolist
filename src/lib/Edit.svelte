<script>
  export let onAdd;
  let inputValue = undefined;

  function handleInputChange(e) {
    let value = e.target.value;
    inputValue = value;
  }

  function handleAdd() {
    // todo:每次添加后 修改container的scrollTop
    if (inputValue == null || inputValue === "") {
      return alert("代办项不能为空，请输入后再添加！");
    }
    onAdd(inputValue);
    inputValue = undefined;
    document.querySelector(".container").scrollTop = 10000000;
  }
</script>

<div>
  <input
    on:input={handleInputChange}
    bind:value={inputValue}
    placeholder="请输入代办项"
  />
  <button on:click={handleAdd}>添加</button>
</div>

<style lang="scss">
  div {
    display: flex;

    input {
      flex: 1;
      height: 31px;
      font-size: 16px;
    }
    button {
      height: 37px;
      margin-left: 10px;
      flex-basis: 70px;
    }
  }
</style>
