<script>
  import ImagePreview from "./ImagePreview.svelte";

  let isDragging = false;
  let files = [];
  let fileInput;
  let showPreview = false;

  function handleDragOver(event) {
    event.preventDefault();
    isDragging = true;
  }

  function handleDragLeave() {
    isDragging = false;
  }

  function handleDrop(event) {
    event.preventDefault();
    isDragging = false;
    files = Array.from(event.dataTransfer.files);
    if (files.length > 0) showPreview = true;
  }

  function handleClick() {
    fileInput.click();
  }

  function handleFileChange(event) {
    files = Array.from(event.target.files);
    if (files.length > 0) showPreview = true;
  }
</script>

{#if !showPreview}
  <!-- Drag and Drop -->
  <div
    role="button"
    tabindex="0"
    on:click={handleClick}
    on:keydown={(event) =>
      (event.key === "Enter" || event.key === " ") && handleClick()}
    on:dragover={handleDragOver}
    on:dragleave={handleDragLeave}
    on:drop={handleDrop}
    class="p-14 border-2 border-dashed border-gray-500 rounded-lg text-center transition-all duration-300"
    class:is-dragging={isDragging}
  >
    <p class="text-gray-500">
      {#if files.length === 0}
        Arrastre y suelte su imagen aquí o haga clic para cargarla.
      {:else}
        {files.length} archivo(s) seleccionado(s).
      {/if}
    </p>
  </div>

  <input
    type="file"
    accept="image/*"
    multiple={false}
    bind:this={fileInput}
    on:change={handleFileChange}
    hidden
  />
{:else}
  <ImagePreview file={files[0]} />
{/if}

<style>
  .is-dragging {
    background-color: #ebf8ff;
    border-color: #4299e1;
  }
</style>
