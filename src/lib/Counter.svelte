<script lang="ts">
  export let currentCount: number = 0
  export let onClickIncrement: () => void
  export let onClickDecrement: () => void
  export let onClickClear: (value: number) => void

  const handleOnClickIncrement = () => {
    onClickIncrement?.()
  }
  const handleOnClickDecrement = () => {
    if(currentCount === 0) return
    onClickDecrement?.()
  }
  const handleOnClickClear = () => {
    onClickClear?.(currentCount)
  }
</script>

<div class={'button-group'}>
  <p>{currentCount}</p>
  <button on:click={handleOnClickIncrement}>
    +
  </button>
  <button on:click={handleOnClickDecrement}>
    -
  </button>
  <button on:click={handleOnClickClear}>
    クリア
  </button>
</div>

<style>
  div.button-group {
    display: flex;
    gap: 4px;
  }
</style>
