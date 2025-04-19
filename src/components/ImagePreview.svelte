<script>
  export let file;

  let imageUrl;

  // Convertimos el archivo en una URL para mostrarlo
  $: if (file) {
    imageUrl = URL.createObjectURL(file);
  }
</script>

<div
  class="max-w-[15rem] max-h-[20rem] overflow-hidden bg-white flex items-center justify-center"
>
  {#if imageUrl}
    <img
      src={imageUrl}
      alt="Imagen cargada"
      class="w-full h-full object-contain"
    />
  {/if}
</div>
