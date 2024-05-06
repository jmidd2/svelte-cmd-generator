<script lang="ts">
  import { cva, type VariantProps } from 'class-variance-authority';
  import type { HTMLButtonAttributes } from 'svelte/elements';

  const baseClass = 'rounded-lg px-3 py-2';

  interface $$Props extends HTMLButtonAttributes, VariantProps<typeof btn> {}

  export let type: 'button' | 'reset' | 'submit' | null | undefined = 'button';
  export let variant: $$Props['variant'] = 'solid';
  export let size: $$Props['size'] = 'small';

  const btn = cva( baseClass, {
    variants: {
      variant: {
        solid: 'bg-blue-gray-700 text-white hover:bg-blue-gray-500 active:bg-blue-gray-700 disabled:bg-blue-gray-950 disabled:text-blue-gray-700',
        outline: 'border border-1 border-blue-gray-600 text-blue-gray-600 hover:text-blue-gray-700 hover:bg-blue-gray-950 hover:border-blue-gray-700 active:border-blue-gray-800 active:text-blue-gray-800 disabled:hover:bg-transparent disabled:border-blue-gray-950 disabled:text-blue-gray-950',
        gradient: 'text-blue-gray-50 bg-gradient-to-b from-blue-gray-500 to-blue-gray-600 hover:ring focus:ring hover:from-blue-gray-600 hover:to-blue-gray-700 disabled:bg-blue-gray-950 disabled:text-blue-gray-700 disabled:bg-none disabled:hover:ring-0'
      },
      size: {
        small: 'text-sm',
        base: 'text-base',
        large: 'text-lg',
      }
    },
  } );
</script>

<button {...$$restProps} class={btn({variant, size, class: $$props.class})} {type}>
    <slot/>
</button>
