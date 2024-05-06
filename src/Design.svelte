<script lang="ts">
  import Button from './lib/Button.svelte';
  import Card from './lib/Card.svelte';

  const options = [
    {
      label: 'Text',
      value: 'text',
    },
    {
      label: 'Label',
      value: 'label',
      indeterminate: true,
    },
    {
      label: 'Label',
      value: 'label',
      disabled: true,
    },
    {
      label: 'Label',
      value: 'label',
      indeterminate: true,
      disabled: true
    }
  ];
</script>

<main class="py-5">
    <div class="container mx-auto space-y-3">
        <div>
            <Button>Normal</Button>
            <Button disabled={true}>Disabled</Button>
            <Button variant="outline">Outline</Button>
            <Button disabled={true} variant="outline">Outline Disabled</Button>
        </div>
        <div>
            <Button variant="gradient">Gradient</Button>
            <Button disabled={true} variant="gradient">Gradient</Button>
        </div>
        <div class="space-y-3">
            <Input.Text/>
            <Input.TextWithLabel label="Test Box" name="test-box"/>
        </div>
        <div>
            <Input.Checkbox label="test" options={options}/>
        </div>
        <div class="flex gap-x-2">
            {#each [ 1, 2, 3 ] as item}
                <Card class="basis-1/3">
                    <h1 slot="header">Header</h1>
                    Body
                </Card>
            {/each}
        </div>
    </div>
</main>
