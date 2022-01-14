<script>
    export let line, number, letterSlice;
</script>

<div class="poem-line">
    <p class="tamil bold">{number}. </p>
    <p class="hl">{line.li.slice(0, letterSlice)}</p>
    <p class="poem">{line.li.slice(letterSlice)}</p>
</div>

<div class="blockquote">
    <p class="tamil bold">பொருள்</p>
    <p class="tamil">{line.pph}</p>

    {#if line.mng}
        {#each line.mng.split(', ') as m}
            <p>{m}</p>
        {/each}
    {/if}
</div>

<div class="blockquote">
    <p class="english bold">English Translation</p>
    <p class="english">{line.tl}</p>
</div>