<script lang="ts">
  import { onMount } from 'svelte';
  import Table from '../components/Table.svelte';
  import Button from '@smui/button';
  import Dialog from '../components/Dialog.svelte';

  type Post = {
    createdAt: Date;
    image: any;
    content: string;
    title: string;
    id: number;
  };

  let items: Post[] = [];
  let loaded = false;

  onMount(() => loadThings(false));

    if (typeof fetch !== 'undefined') {
      loaded = false;

      fetch('https://api.fake-rest.refine.dev/posts')
        .then((response) => response.json())
        .then((json) => 
          setTimeout (
            () => {
              items = json;
              loaded = true;
            },
            // Simulate a long load time.
            wait ? 2000 : 0
        )
      );
    }
  };
</script>

let open = false;

<div style="display: flex; justify-content: space-between;">
  <Button on:click={() => (open = true)}>Add New</Button>
</div>

<Table {items} {loaded} />

<Dialog {open} />
