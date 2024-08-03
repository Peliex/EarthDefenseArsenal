<script>
    import MissionTable from './missionchecklist/MissionTable.svelte';
    import WeaponTable from './missionchecklist/WeaponTable.svelte';

    let selectedMission = null;
    let selectedDifficulty = null;
    let filteredWeapons = [];

    function handleSelect(event)
    {
        console.log(`${event.detail.mission.name}`);
        selectedMission = event.detail.mission;
        selectedDifficulty = event.detail.difficulty;
        filteredWeapons = event.detail.filteredWeapons;
    }
</script>

<main>
    <MissionTable on:select={handleSelect} />
    <WeaponTable {selectedMission} {selectedDifficulty} {filteredWeapons} />
</main>

<style>
    main
    {
        background-color: #505050;
        color: white;
        display: flex;
        flex-direction: row;
        gap: 20px;
    }
</style>
