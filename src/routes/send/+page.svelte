<script lang="ts">
    let files: FileList | null | undefined = $state();

    $effect(() => {
        if (files) {
            const file: File = files.item(0)!
            console.log(file.type)
        }
    });
</script>

<input bind:files type="file" />
