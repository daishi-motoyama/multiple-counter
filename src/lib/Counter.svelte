<script lang="ts">
  export let currentCount: number = 0
  export let onClickIncrement: () => void
  export let onClickDecrement: () => void
  export let onClickClear: (value: number) => void

  const handleOnClickIncrement = () => {
    onClickIncrement?.()
  }
  const handleOnClickDecrement = () => {
    if (currentCount === 0) return
    onClickDecrement?.()
  }
  const handleOnClickClear = () => {
    onClickClear?.(currentCount)
  }
</script>

<div class="flex items-center gap-6">
  <p>{currentCount}</p>
  <div class="flex gap-2">
    <button
      class="bg-green-500 hover:bg-green-400 text-white rounded px-3 py-1"
      on:click={handleOnClickIncrement}
    >
      +
    </button>
    <button
      class="bg-blue-500 hover:bg-blue-400 text-white rounded px-3 py-1"
      on:click={handleOnClickDecrement}
    >
      -
    </button>
    <button
      class="bg-yellow-500 hover:bg-yellow-400 text-white rounded px-2 py-1"
      on:click={handleOnClickClear}
    >
      0
    </button>
  </div>
</div>
