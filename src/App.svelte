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
  const handleOnAddNewField = () => {
    counters = [...counters, {count: INITIAL_COUNTERS_COUNT, title: INITIAL_COUNTERS_TITLE}]
  }
</script>

<main>
  <h1>Multiple Counter</h1>
  {#each counters as counter, index}
    <input bind:value={counter.title}/>
    <Counter currentCount={counter.count} onClickIncrement={() => counter.count++} onClickDecrement={() => counter.count--} onClickClear={() => counter.count = 0} />
    <button on:click={() => counters = counters.filter((_, _index) => _index !== index)}>
      ✗
    </button>
  {/each}
  <p>
    title: {counters.map((counter) => counter.title)}
  </p>
  <p>{totalCount}</p>
  <button on:click={handleOnAddNewField}>
    New Field
  </button>
</main>