<script lang="ts">
  import type { ComponentEvents } from 'svelte';
  import type { OptionType } from './index';
  import Card from './lib/Card.svelte';
  import Checkbox from './lib/Input/Checkbox.svelte';
  import TextboxWithLabel from './lib/Input/TextboxWithLabel.svelte';

  let command = 'rsync';

  let checkedValues: OptionType[] = [];

  const rsyncOptions: OptionType[] = [
    {
      label: 'verbose',
      value: 'verbose',
      singleDash: 'v',
      doubleDash: 'verbose',
      description: 'Makes more output.'
    }, {
      label: 'archive',
      value: 'archive',
      singleDash: 'a',
      doubleDash: 'archive',
      description: 'Makes more output.'
    }, {
      label: 'compress',
      value: 'compress',
      singleDash: 'z',
      doubleDash: 'compress',
      description: 'Makes more output.'
    }, {
      label: 'dry run',
      value: 'dry-run',
      singleDash: 'n',
      doubleDash: 'dry-run',
      description: 'Makes more output.'
    }, {
      label: 'checksum',
      value: 'checksum',
      singleDash: 'c',
      doubleDash: 'checksum',
      description: 'Makes more output.'
    }, {
      label: 'recursive',
      value: 'recursive',
      singleDash: 'r',
      doubleDash: 'recursive',
      description: 'Makes more output.'
    }, {
      label: 'update',
      value: 'update',
      singleDash: 'u',
      doubleDash: 'update',
      description: 'Makes more output.'
    }, {
      label: 'human-readable',
      value: 'human-readable',
      singleDash: 'h',
      doubleDash: 'human-readable',
      description: 'Makes more output.'
    }, {
      label: 'progress',
      value: 'progress',
      doubleDash: 'progress',
      description: 'Makes more output.'
    }, {
      label: 'partial',
      value: 'partial',
      doubleDash: 'partial',
      description: 'Makes more output.'
    }, {
      label: 'partial-dir',
      value: 'partial-dir',
      doubleDash: 'partial-dir',
      description: 'Makes more output.'
    }, {
      label: 'partial progress',
      value: 'partial-progress',
      singleDash: 'P',
      description: 'Makes more output.'
    }
  ];

  let newString = '';
  let singleDashOptions = '-';
  let doubleDashOptions = '';

  function handleCheckboxChange( event: ComponentEvents<Checkbox>['newValue'] ) {
    console.log( event );
    newString = '';
    singleDashOptions = '';
    command = 'rsync';
    doubleDashOptions = '';

    checkedValues = event.detail;

    if ( checkedValues.length > 1 ) {
      singleDashOptions = '-';
    }

    for ( const opt of checkedValues ) {
      if ( checkedValues.length > 1 ) {
        newString += `${ opt.value } `;
        if ( opt.singleDash ) {
          newString += `-${ opt.singleDash } `;
          singleDashOptions += `${ opt.singleDash }`;
        }
        if ( !opt.singleDash && opt.doubleDash ) {
          newString += `--${ opt.doubleDash } `;
          if ( doubleDashOptions === '' ) {
            doubleDashOptions += `--${ opt.doubleDash }`;
          }
          else {
            doubleDashOptions += ` --${ opt.doubleDash }`;
          }
        }
      }
      else {
        newString = opt.value;
        if ( opt.singleDash ) {
          newString += ` -${ opt.singleDash } `;
          singleDashOptions += `-${ opt.singleDash }`;
        }
        if ( opt.doubleDash ) {
          newString += `--${ opt.doubleDash } `;
        }
      }
    }

    command += ` ${ singleDashOptions } ${ doubleDashOptions }`;
  }
</script>

<div class="container mx-auto py-16">
    <div class="top-header"><h2 class="text-4xl font-bold tracking-tight text-white sm:text-6xl">RSYNC Command
        Generator</h2></div>
    <main class="content">
        <div>
            <TextboxWithLabel label="RSYNC Command" name="command" value={command}/>
            <p class="mt-3">Checked Values:
                {#each checkedValues as value}{value.value} {/each}
            </p>
            <p class="mt-3">{newString}</p>
            <p class="mt-3">
                {#if singleDashOptions !== '-'}{singleDashOptions}{/if}
            </p>
        </div>
        <div class="options">
            <Card class="origin">
                <h1 slot="header">Origin</h1>
                <div>
                    Login
                </div>
                <div>
                    Host
                </div>
                <div>
                    Path
                </div>
            </Card>
            <Card class="Destination row-span-2">
                <h1 slot="header">Settings</h1>
                <div>
                    Port
                </div>
                <div>
                    All the checkboxes for the manpage options
                    <Checkbox on:newValue={handleCheckboxChange} options={rsyncOptions}/>
                </div>
            </Card>
            <Card class="Destination">
                <h1 slot="header">Destination</h1>
                <div>
                    Login
                </div>
                <div>
                    Host
                </div>
                <div>
                    Path
                </div>
            </Card>
        </div>
    </main>
</div>

<style>
    .content {
        @apply my-6 space-y-6;
    }

    .options {
        @apply grid grid-cols-2 gap-6;
    }
</style>
