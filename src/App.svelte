<script lang="ts">
  import Counter from './lib/Counter.svelte'
  const INITIAL_COUNTERS_COUNT = 0
  const INITIAL_COUNTERS_TITLE = 'new'
  let counters = [
    {
      count: INITIAL_COUNTERS_COUNT,
      title: INITIAL_COUNTERS_TITLE
    }
  ]
  $: totalCount = counters.reduce((previousCount, currentCounter) => previousCount + currentCounter.count, 0)
  const handleOnDeleteField = (targetFieldIndex: number) => {
    counters = counters.filter((_, index) => index !== targetFieldIndex)
  }
  const handleOnAddNewField = () => {
    counters = [...counters, {count: INITIAL_COUNTERS_COUNT, title: INITIAL_COUNTERS_TITLE}]
  }
</script>

<main class="text-center grid max-w-md gap-4 mx-auto">
  <h1 class="text-2xl font-black">Multiple Counter</h1>
  <div class="grid gap-4">
    {#each counters as counter, index}
      <div class="bg-gray-50 flex justify-center items-center gap-2 p-2 rounded shadow-lg">
        <input class="border border-gray-300 text-sm rounded px-2 py-1" bind:value={counter.title}/>
        <Counter currentCount={counter.count} onClickIncrement={() => counter.count++} onClickDecrement={() => counter.count--} onClickClear={() => counter.count = 0} />
        <button class="bg-red-500 hover:bg-red-400 text-white rounded px-3 py-1" on:click={() => handleOnDeleteField(index)}>
          削除
        </button>
      </div>
    {/each}
    <button class="bg-green-200 hover:bg-green-100 rounded w-full px-2 py-1" on:click={handleOnAddNewField}>
      新しいカウンターを追加
    </button>
    <div class="grid gap-2">
      <p>
        フィールドタイトル: {counters.map((counter) => counter.title)}
      </p>
      <p>合計カウント：{totalCount}</p>
    </div>
  </div>
</main>
