<!-- Reflection.svelte -->
<script>
    export let dailyReflection;
</script>

<div class="daily-reflection">
    <h3>End of the Day Thoughts</h3>
    <textarea bind:value={dailyReflection} placeholder="What made your day unique today?"></textarea>
</div>

<style>
    textarea {
        width: 100%;
        padding: 0.5rem;
        border: 1px solid #ddd;
        border-radius: 8px;
        min-height: 100px;
    }
</style>
