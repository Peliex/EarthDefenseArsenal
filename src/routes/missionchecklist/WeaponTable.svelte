<!--
@component

- Renders tables for each character class based on provided mission and difficulty

@example
```svelte
<WeaponTable selectedMission={mission} selectedDifficulty={difficulty} filteredWeapons={filterResult}/>
```
-->
<script>
    export let selectedMission = null;
    export let selectedDifficulty = null;
    export let filteredWeapons = [];
</script>

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
</style>
