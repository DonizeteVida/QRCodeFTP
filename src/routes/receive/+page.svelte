<script lang="ts">
    import { onMount } from "svelte";

    import { BrowserQRCodeReader } from "@zxing/browser";

    const reader = new BrowserQRCodeReader(new Map(), {
        delayBetweenScanSuccess: 0,
        delayBetweenScanAttempts: 0,
    });

    let stream: HTMLVideoElement;

    onMount(async () => {
        reader.decodeFromConstraints(
            {
                video: true,
            },
            stream,
            (result, error, controls) => {
                if (result) {
                    console.log(result.getText());
                }
            },
        );
    });
</script>

<video bind:this={stream}>
    <track kind="captions" />
</video>
