<script>
    import { onMount } from 'svelte';
    export let name;
    let kofiReady = false;
    let mounted = false;
    onMount(() => {
      mounted = true;
      // if (kofiReady) {
      setTimeout(() => loadKofiWidget(), 1000);
      // }
    });
    function kofiLoaded() {
      kofiReady = true;
      if (mounted) {
        loadKofiWidget();
      }
    }
    function loadKofiWidget() {
      window.kofiWidgetOverlay?.draw(
        name,
        {
          type: 'floating-chat',
          'floating-chat.donateButton.text': 'Support me',
          'floating-chat.donateButton.background-color': '#4c4c4c',
          'floating-chat.donateButton.text-color': '#fff',
        },
        'kofiContainer'
      );
    }
  </script>
  <svelte:head>
    <script
      async
      defer
      type="text/javascript"
      src="https://storage.ko-fi.com/cdn/scripts/overlay-widget.js"
      on:load={kofiLoaded}></script>
  </svelte:head>
  {#if name}
    <div id="kofiContainer" class="web-only" />
  {/if}