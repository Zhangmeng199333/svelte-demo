<script>
  import { createEventDispatcher } from 'svelte'
  import { onMount } from 'svelte'
  let title = 'hello svelte'
  onMount(() => {
    console.log('onMount')
    setTimeout(() => {
      title = 'vue ==> svelte'
    }, 2000)
  })
  const dispatch = createEventDispatcher()
  const printPhone = () => {
    dispatch('printPhone', '199999999')
  }
</script>

<button on:click={printPhone}>输出手机号码</button>

<div class="box">
  <slot>默认值</slot>
</div>
<h1>{title}</h1>

<style>
  .box {
    width: 300px;
    height: 100px;
    font-size: 20px;
    margin: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
    border: 1px solid #aaa;
    border-radius: 5px;
    box-shadow: 2px 2px 18px #aaa;
  }
</style>
