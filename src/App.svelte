<script>
    import Footer from './Footer.svelte';
    import Line from './Line.svelte';

    let loaded = null;
    let section = null;

    fetch(`${window.location.href}/aathichudi.json`)
        .then(res => res.json())
        .then(body => {
            loaded = body;
            section = loaded.sections[0];
        });
</script>

<div class="cover" id="cover">
    <h1>ஆத்திசூடி</h1>
    <p>ஔவையாரின் ஆத்திசூடி / Avvaiyar's Aathichudi</p>
</div>

<div class="content" id="content">
    {#if !loaded}
        <p class="tamil">சிறிது நேரம் காத்திருக்கவும்...</p>
        <p class="english">Please wait for some time...</p>
    {:else}
        <h2 class="tamil">கடவுள் வாழ்த்து / Compliment to Lord</h2>

        <div class="content-box">
            {#each loaded.kadavul_vazhthu.line.split('\n') as line}
                <p class="tamil poem">{line}</p>
            {/each}

            <div class="blockquote">
                <p class="tamil bold">பொருள்</p>
                <p class="tamil">{loaded.kadavul_vazhthu.porul}</p>
            </div>

            <div class="blockquote">
                <p class="english bold">English Transliteration</p>
                {#each loaded.kadavul_vazhthu.transliteration.split('\n') as line}
                    <p class="english">{line}</p>
                {/each}
            </div>
        </div>

        <div id="aks"></div>

        <h2 class="tamil">{section.name} / {section.transliteration}</h2>

        {#each loaded.lines.slice(section.lines[0] - 1, section.lines[1]) as line, i}
            <div class="content-box">
                <!-- A lot of mess here... Try to clean if possible... -->
                <Line 
                    line={line} 
                    number={section.lines[0] + i}
                    letterSlice={Number(!line.lslice) + 1}
                />
            </div>
        {/each}

        <h2 class="tamil">பொருளடக்கம் / Index</h2>

        <div class="content-box">
            {#each loaded.sections as sec, i}
                <h3 
                    on:click={() => {
                        document.getElementById('aks').scrollIntoView();
                        section = loaded.sections[i];
                    }}
                >
                    {sec.name} / {sec.transliteration} 
                </h3>
            {/each}
        </div>
    {/if}
</div>

<Footer/>