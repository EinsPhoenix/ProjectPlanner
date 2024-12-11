<script lang="ts">
    import { createEventDispatcher } from "svelte";

    const dispatch = createEventDispatcher();

    // Event Dispatcher zum Handhaben der Klicks
    const handleHomeClick = () => dispatch("homeClick");
    const handlePlaceholderClick = () => dispatch("placeholderClick");
    const handleSettingsClick = () => dispatch("settingsClick");
</script>

<header>
    <div class="left">
        <button class="project-planner">Project Planner</button>
    </div>

    <div class="center"></div>

    <div class="right">
        <button class="home" on:click={handleHomeClick}>
            <img src="/icons/home.svg" alt="Home" />
        </button>
        <button class="placeholder" on:click={handlePlaceholderClick}>
            <img src="/icons/placeholder.svg" alt="Placeholder" />
        </button>
        <button class="settings" on:click={handleSettingsClick}>
            <img src="/icons/settings.svg" alt="Settings" />
        </button>
    </div>
</header>

<style>
    header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 1rem;
        background-color: #333;
        color: white;
    }

    .left {
        flex: 1;
        display: flex;
        justify-content: flex-start;
    }

    .center {
        flex: 2;
        display: flex;
        justify-content: center;
    }

    .right {
        display: flex;
        justify-content: flex-end;
        gap: 1rem;
    }

    button {
        background: none;
        border: none;
        color: white;
        cursor: pointer;
    }

    button img {
        width: 24px;
        height: 24px;
    }

    .project-planner {
        font-size: 1.2rem;
        font-weight: bold;
    }
</style>
