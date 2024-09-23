<!-- ImageUpload.svelte -->
<script>

    /*
     * Name: Anay Abhijit Joshi
     * CS 5167: User Interface 1
     * Level: Undergraduate Student
     */

    export let image;
    // export let dailyReflection;
</script>

<div class="image-upload and caption entry">
    <h3>Share your Captured Moment and Add a Caption</h3>
    <input type="file" bind:value={image} accept="image/*">
    <!-- <textarea bind:value={dailyReflection} placeholder="Describe your picture or why it's meaningful to you?"></textarea> -->
</div>

<style>
    input[type="file"] {
        width: 100%;
        padding: 0.5rem;
        border: 1px solid #ddd;
        border-radius: 8px;
        margin-top: 0.25rem;
    }
</style>
