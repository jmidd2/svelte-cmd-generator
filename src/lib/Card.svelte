<script lang="ts">

  import { twMerge } from 'tailwind-merge';
</script>

<div class={twMerge($$props.class, 'card')}>
    <div class="card-header">
        <slot name="header"/>
    </div>
    <div class="card-body">
        <slot/>
    </div>
</div>

<style>
    .card {
        @apply flex flex-col;
    }

    .card-header {
        @apply text-xl rounded-t-lg p-2 font-bold bg-blue-gray-800 text-white;
    }

    .card-body {
        @apply bg-zinc-800 text-blue-gray-100 p-2 text-sm flex-grow;
    }
</style>
