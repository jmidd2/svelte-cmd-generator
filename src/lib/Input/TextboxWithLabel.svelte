<script lang="ts">
  import Textbox from './Textbox.svelte';

  export let id: string | null = null;
  export let name: string;
  export let label: string;
  export let value: string;

  export let variant: 'base' | 'large' | 'small' | null | undefined = 'base';

  if ( !id && name ) {
    id = name;
  }
</script>

<div>
    <label class="mb-1 block text-sm font-medium text-blue-gray-200" for={id}>{label}</label>
    <Textbox {...$$restProps} {id} {name} {value} {variant}/>
</div>
