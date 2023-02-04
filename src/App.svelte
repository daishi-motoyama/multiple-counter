<script lang="ts">
  import Counter from "./lib/Counter.svelte"
  const INITIAL_COUNTERS_COUNT = 0
  const INITIAL_COUNTERS_TITLE = "new"
  let counters = [
    {
      count: INITIAL_COUNTERS_COUNT,
      title: INITIAL_COUNTERS_TITLE,
    },
  ]
  $: totalCount = counters.reduce(
    (previousCount, currentCounter) => previousCount + currentCounter.count,
    0
  )
  const handleOnDeleteField = (targetFieldIndex: number) => {
    counters = counters.filter((_, index) => index !== targetFieldIndex)
  }
  const handleOnAddNewField = () => {
    counters = [
      ...counters,
      { count: INITIAL_COUNTERS_COUNT, title: INITIAL_COUNTERS_TITLE },
    ]
  }
</script>

<main class="mx-auto grid max-w-md gap-4 text-center">
  <h1 class="text-2xl font-black">Multiple Counter</h1>
  <div class="grid gap-4">
    {#each counters as counter, index}
      <div
        class="flex items-center justify-center gap-2 rounded bg-gray-50 p-2 shadow-lg"
      >
        <input
          class="rounded border border-gray-300 px-2 py-1 text-sm"
          bind:value={counter.title}
        />
        <Counter
          currentCount={counter.count}
          onClickIncrement={() => counter.count++}
          onClickDecrement={() => counter.count--}
          onClickClear={() => (counter.count = 0)}
        />
        <button
          class="rounded bg-red-500 px-3 py-1 text-white hover:bg-red-400"
          on:click={() => handleOnDeleteField(index)}
        >
          削除
        </button>
      </div>
    {/each}
    <button
      class="w-full rounded bg-green-200 px-2 py-1 hover:bg-green-100"
      on:click={handleOnAddNewField}
    >
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
