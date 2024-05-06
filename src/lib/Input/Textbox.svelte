<script lang="ts">
  import { cva, type VariantProps } from 'class-variance-authority';
  import type { HTMLInputAttributes, HTMLInputTypeAttribute } from 'svelte/elements';
  import { twJoin } from 'tailwind-merge';

  export let value: string = '';
  export let type: HTMLInputTypeAttribute | null = 'text';

  const TEXT_BASE_CLASS = 'input text-blue-gray-900 block w-full rounded-md border-gray-300 shadow-sm';
  const TEXT_FOCUS_CLASS = 'focus:border-blue-gray-400 focus:ring focus:ring-blue-gray-200 focus:ring-opacity-50';
  const TEXT_DISABLED_CLASS = 'disabled:cursor-not-allowed disabled:bg-gray-50 disabled:text-gray-500';

  interface $$Props extends HTMLInputAttributes, VariantProps<typeof inputText> {}

  export let variant: $$Props['variant'] = 'base';

  const inputText = cva( twJoin( TEXT_BASE_CLASS, TEXT_FOCUS_CLASS, TEXT_DISABLED_CLASS ), {
    variants: {
      variant: {
        base: 'text-base',
        large: 'text-lg',
        small: 'text-sm',
      },
    },
  } );

</script>

<input {...$$restProps} class={inputText({variant, class: $$props.class})} {type} {value}/>
