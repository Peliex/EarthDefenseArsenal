<script>
    import { createEventDispatcher } from 'svelte';
    import { missions } from '../../lib/missions.js';
    import { weapons as Fencer } from '../../lib/fencer.js'

    const dispatch = createEventDispatcher();

    function selectDifficulty(mission, difficulty, index)
    {   
        const minLevel = mission.minimumLevel[index];
        const maxLevel = mission.maximumLevel[index];

        const filteredWeapons = Fencer.filter(weapon => 
            weapon.level >= minLevel && weapon.level <= maxLevel
        );
        console.log(`${mission.name}, ${difficulty}`)
        dispatch('select', {mission, difficulty, filteredWeapons});
    }
</script>

<table>
    <thead>
        <tr>
            <th style="background-color: black; text-align: center;" colspan="6">EDF 6 Missions</th>
        </tr>
        <tr>
            <th rowspan="2">Number</th>
            <th rowspan="2">Mission Name</th>
            <th style="text-align:center;" colspan="4">Item Level Range</th>
        </tr>
        <tr>
            <th>Normal</th>
            <th>Hard</th>
            <th>Hardest</th>
            <th>Inferno</th>
        </tr>
    </thead>
    <tbody>
        {#each missions as mission}
            <tr>
                <td class="td-number">{mission.number}</td>
                <td>{mission.name}</td>
                {#if mission.minimumLevel}
                    <td style="text-align: center" class="td-difficulty-normal" on:click={() => selectDifficulty(mission, 'Normal', 0)}>{mission.minimumLevel[0]} - {mission.maximumLevel[0]}</td>
                    <td style="text-align: center" class="td-difficulty-hard" on:click={() => selectDifficulty(mission, 'Hard', 1)}>{mission.minimumLevel[1]} - {mission.maximumLevel[1]}</td>
                    <td style="text-align: center" class="td-difficulty-hardest" on:click={() => selectDifficulty(mission, 'Hardest', 2)}>{mission.minimumLevel[2]} - {mission.maximumLevel[2]}</td>
                    <td style="text-align: center" class="td-difficulty-inferno" on:click={() => selectDifficulty(mission, 'Inferno', 3)}>{mission.minimumLevel[3]} - {mission.maximumLevel[3]}</td>
                {:else}
                    <td style="background-color: black;" class="td-difficulty-normal" colspan=4 />
                {/if}
            </tr>
        {/each}
    </tbody>
</table>

<style>
    table
    {
        border-collapse: collapse;
        font-family: Arial, Helvetica, sans-serif;
    }

    th, td
    {
        border: 1px solid black;
        padding: 8px;
    }

    th
    {
        background-color: darkslategray
    }

    .td-number
    {
        background-color: darkslategray;
        font-size: x-large
    }

    .td-difficulty-normal
    {
        background-color:lightgreen;
        color: darkred;
    }

    .td-difficulty-hard
    {
        background-color: palegoldenrod;
        color: darkviolet;
    }

    .td-difficulty-hardest
    {
        background-color: lightsalmon;
        color: darkmagenta;
    }

    .td-difficulty-inferno
    {
        background-color: lightcoral;
        color: rgb(0, 49, 0)
    }
</style>
