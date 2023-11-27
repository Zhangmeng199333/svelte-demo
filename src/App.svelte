<script>
  import Counter from './lib/Counter.svelte'
  import Phone from './components/phone/index.svelte'
  import FatherChild from './components/commucate/index.svelte'
  let name = '小鱼儿'
  const handleClick = () => {
    name = '大鱼儿'
  }
  const doSomething = () => {
    return `${name},你好！`
  }
  let a = 1,
    b = 2
  let state = false
  // 渲染HTML标签 @html
  let el = '<h1 style="color:pink;">小鱼儿</h1>'
  // 行内样式style
  let color = 'red'
  setTimeout(() => {
    color = 'blue'
  }, 1000)
  let foo = true
  setTimeout(() => {
    foo = false
  }, 2000)
  // 条件渲染
  setTimeout(() => {
    state = true
  }, 4000)
  let count = 0
  setInterval(() => {
    count++
  }, 1000)
  // 列表渲染
  let list = [1, 2, 3, 4, 5]
  // 支持对象解构
  let user = [
    { name: 'jude', age: 18 },
    { name: 'summer', age: 24 }
  ]
  // 默认内容
  let arr = []
  // 事件
  const sayHello = () => {
    console.log('hello')
  }
  // 数据绑定
  let message = '数据绑定'
  const print = () => {
    console.log(message)
  }
  // 数据双向绑定
  const showChangeValue = () => {
    console.log(message)
  }
  // input range 范围选择
  let val = 0
  let selected = '1'
  let roles = []
  let selectedRole = 'a'
  let selectedRoleList = []
  // $:声明反应性
  let number = 0
  $: numbers = number * 2
  const handledbClick = () => {
    number += 1
  }
  const data = new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve('123')
    }, 1000)
  })
  const printPhoneNumber = (data) => {
    console.log('data', `手机号码:${data.detail}`)
  }
</script>

<main>
  <div class="card">
    <Counter />
    <h1>hello {name}</h1>
    <button on:click={handleClick}>Change Name</button>
    <div>{doSomething()}</div>
    <div>{a} + {b} = {a + b}</div>
    <div>{state ? '小鱼儿' : '大鱼儿'}</div>
    <div>{@html el}</div>
    <div style="color:{color}">小鱼儿</div>
    <div class:active={foo}>小鱼儿</div>
    {#if state}
      <div>小鱼儿</div>
    {:else}
      <div>大玉儿</div>
    {/if}
    {#if count === 0}
      <div>0</div>
    {:else if count === 1}
      <div>1</div>
    {:else if count === 2}
      <div>2</div>
    {/if}
    <ul>
      {#each list as item, index}
        <li>{index + 1} --- {item}</li>
      {/each}
    </ul>
    <ul>
      {#each user as { name, age }}
        <li>{name}-{age}</li>
      {/each}
    </ul>
    {#each arr as { name }}
      <div>{name}</div>
    {:else}
      <div>暂无数据</div>
    {/each}
    <button on:click|once={sayHello}>hello</button>
    <input type="text" on:input={showChangeValue} bind:value={message} />
    <button on:click={print}>print</button>
    <textarea bind:value={message} name="" id="" cols="30" rows="3" />
    <p>{message}</p>
    <input type="range" bind:value={val} min="0" max="10" />
    <p>{val}</p>
    <input type="radio" bind:group={selected} value="1" />
    <input type="radio" bind:group={selected} value="2" />
    <input type="radio" bind:group={selected} value="3" />
    <p>{selected}</p>
    <input type="checkbox" bind:group={roles} value="yu" />
    <input type="checkbox" bind:group={roles} value="qi" />
    <input type="checkbox" bind:group={roles} value="jude" />
    <input type="checkbox" bind:group={roles} value="summer" />
    <p>{roles}</p>
    <select bind:value={selectedRole}>
      <option value="a">a</option>
      <option value="b">b</option>
      <option value="c">c</option>
    </select>
    <span>{selectedRole}</span>
    <select multiple bind:value={selectedRoleList}>
      <option value="a">a</option>
      <option value="b">b</option>
      <option value="c">c</option>
    </select>
    <p>{selectedRoleList}</p>
    <button on:click={handledbClick}>add </button>
    <p>{number} ==> {numbers}</p>
    {#await data}
      <span>loading...</span>
    {:then res}
      <span>{res}</span>
    {:catch err}
      <span>{err}</span>
    {/await}
    <p>组件</p>
    <Phone phone="9999" />
    <br />
    <FatherChild on:printPhone={printPhoneNumber}>
      <div>电话：</div>
      <div>1999999999999</div>
    </FatherChild>
  </div>
</main>

<style>
  .active {
    color: red;
  }
</style>
