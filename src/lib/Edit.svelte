<script>
  export let handleAdd;
  let inputValue = undefined;
  function handleInputChange(e) {
    inputValue = e.target.value;
  }
</script>

<div>
  <!-- 
    on:input + bind:value 双向绑定
   -->
  <input
    on:input={handleInputChange}
    bind:value={inputValue}
    placeholder="请输入代办项"
  />
  <button
    on:click={() => {
      handleAdd(inputValue);
      inputValue = undefined;
    }}>添加</button
  >
</div>

<style lang="scss">
  div {
    padding-top: 20px;
    input {
      width: 60%;
      height: 31px;
      font-size: 16px;
    }
  }
</style>
