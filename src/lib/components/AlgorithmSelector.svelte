<script lang="ts">
  export let selectAlgorithm: (algo: AlgorithmDefinition) => void;
  export let selectedAlgorithm: AlgorithmDefinition;

  import { algorithms } from '../sort-algorithms/algorithms';
  import type { AlgorithmDefinition } from '../sort-algorithms/types';
  import ArrowRight from './algorithm-selector/ArrowRight.svelte';
  import ArrowLeft from './algorithm-selector/ArrowLeft.svelte';

  const click = (algo: AlgorithmDefinition) => () => {
    selectAlgorithm(algo);
  };
</script>

<div class="flex bg-base-200 rounded-box mb-2 md:mb-0 md:mr-5">
  <div class="carousel rounded-box md:w-[30.5rem]">
    {#each algorithms as algos, group}
      <div id="group{group}" class="carousel-item w-full">
        <ul class="menu flex flex-row md:grid md:grid-rows-4 grid-flow-col">
          {#each algos as algo, index}
            <li>
              <button
                class={algo.name === selectedAlgorithm?.name ? 'active' : ''}
                on:click={click(algo)}>{algo.name}</button
              >
            </li>
            {#if index === 2 && group > 0}
              <ArrowLeft {group} />
            {/if}
          {/each}
          {#if group !== algorithms.length - 1}
            <ArrowRight {group} />
          {/if}
        </ul>
      </div>
    {/each}
  </div>
</div>
