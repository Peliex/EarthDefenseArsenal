<script>
    import { missions } from '../../lib/missions.js';
    import { weapons as Fencer } from '../../lib/fencer.js'

    let selectedMission = null;
    let selectedDifficulty = null;
    let filteredWeapons = [];

    function selectDifficulty(mission, difficulty, index)
    {
        selectedMission = mission;
        selectedDifficulty = difficulty;
        const minLevel = mission.minimumLevel[index];
        const maxLevel = mission.maximumLevel[index];

        filteredWeapons = Fencer.filter(weapon => 
            weapon.level >= minLevel && weapon.level <= maxLevel
        );
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
                <td style="text-align: center" class="td-difficulty-normal" on:click={() => selectDifficulty(mission, 'Normal', 0)}>{mission.minimumLevel[0]} - {mission.maximumLevel[0]}</td>
                <td style="text-align: center" class="td-difficulty-hard" on:click={() => selectDifficulty(mission, 'Hard', 1)}>{mission.minimumLevel[1]} - {mission.maximumLevel[1]}</td>
                <td style="text-align: center" class="td-difficulty-hardest" on:click={() => selectDifficulty(mission, 'Hardest', 2)}>{mission.minimumLevel[2]} - {mission.maximumLevel[2]}</td>
                <td style="text-align: center" class="td-difficulty-inferno" on:click={() => selectDifficulty(mission, 'Inferno', 3)}>{mission.minimumLevel[3]} - {mission.maximumLevel[3]}</td>
            </tr>
        {/each}
    </tbody>
</table>

{#if selectedMission && selectedDifficulty}
    <div>
        <h2>Weapons available on {selectedMission.name} ({selectedDifficulty} Difficulty)</h2>
        <div class="weapon-table">
            <table>
                <thead>
                    <tr>
                        <th colspan=4><h3>Fencer</h3></th>
                    </tr>
                    <tr>
                        <th>Weapon Name</th>
                        <th>Level</th>
                        <th>Stars</th>
                        <th>Weapon Type</th>
                    </tr>
                </thead>
                <tbody>
                    {#each filteredWeapons as weapon}
                        <tr>
                            <td>{weapon.name}</td>
                            <td>{weapon.level}</td>
                            <td>{weapon.stars}</td>
                            <td>{weapon.type}</td>
                        </tr>
                    {/each}
                </tbody>
            </table>
        </div>
    </div>
{/if}

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
