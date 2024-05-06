<script lang="ts">
  import { createEventDispatcher } from 'svelte';
  import { twJoin } from 'tailwind-merge';
  import type { OptionType } from '../../index';

  export let options: OptionType[] = [];

  const dispatch = createEventDispatcher();

  const CHECK_BASE_CLASS = 'peer h-4 w-4 rounded border-gray-300 text-blue-gray-700 shadow-sm';
  const CHECK_DISABLED_CLASS = 'disabled:cursor-not-allowed disabled:text-gray-500';
  const CHECK_FOCUS_CLASS = 'focus:border-blue-gray-300 focus:ring focus:ring-blue-gray-200 focus:ring-opacity-50 focus:ring-offset-0';
  const LABEL_BASE_CLASS = 'peer-disabled:text-gray-500 text-sm font-medium text-blue-gray-400';

  let checkedValues: OptionType[] = [];

  function handleChange( event: Event, option: OptionType ) {
    const target = event.target as HTMLInputElement;
    if ( target.checked ) {
      if ( option.value === 'partial-progress' ) {
        checkedValues = checkedValues.filter( opt => opt.value !== 'partial' && opt.value !== 'progress' );
        console.log( checkedValues );
        const progressCheckbox = document.getElementById( 'progress' ) as HTMLInputElement;
        const partialCheckbox = document.getElementById( 'partial' ) as HTMLInputElement;

        if ( progressCheckbox && partialCheckbox ) {
          progressCheckbox.checked = true;
          partialCheckbox.checked = true;
        }
      }
      checkedValues.push( option );
    }
    else {
      checkedValues = checkedValues.filter( opt => opt.value !== option.value );
    }
    dispatch( 'newValue', checkedValues );
  }
</script>

<div class="space-y-3">
    {#each options as option}
        <div class="flex items-center space-x-2">
            <input {...$$restProps} on:change={(e) => handleChange(e, option)} disabled={option.disabled}
                   indeterminate={option.indeterminate} value={option.value} type="checkbox" id={option.value}
                   class={twJoin(CHECK_BASE_CLASS, CHECK_DISABLED_CLASS, CHECK_FOCUS_CLASS)}/>
            <label for="example1" class={LABEL_BASE_CLASS}>{option.label}</label>
        </div>
    {/each}
</div>
