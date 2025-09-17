<script lang="ts">
    let stream: HTMLVideoElement;

    $effect(() => {
        navigator.mediaDevices
            .getUserMedia({
                video: true,
            })
            .then((value) => (stream.srcObject = value))
            .then(() => stream.play());
    });
</script>

<video bind:this={stream}>
    <track kind="captions" />
</video>