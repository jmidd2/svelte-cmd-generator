<script lang="ts">
  import Button from './lib/Button.svelte';
</script>

<main class="py-5">
    <div class="container mx-auto">
        <Button>Normal</Button>
        <Button disabled={true}>Disabled</Button>
        <Button variant="outline">Outline</Button>
        <Button disabled={true} variant="outline">Outline Disabled</Button>

        <Button variant="gradient">Gradient</Button>
    </div>
</main>

<style>

</style>
