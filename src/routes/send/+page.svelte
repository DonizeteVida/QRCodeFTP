<script lang="ts">
    import { BrowserQRCodeSvgWriter } from "@zxing/browser";

    let bufferSize = $state(16);

    const qrCodeWriter = new BrowserQRCodeSvgWriter();

    let files: FileList | null | undefined = $state();

    let qrCodeArea: HTMLElement;

    $effect(() => {
        if (files) {
            const file = files.item(0);
            if (file) writeFile(file);
        }
    });

    const delay = (ms: number) => new Promise((res) => setTimeout(res, ms));

    async function writeFile(file: File) {
        let index = 0;
        const decoder = new TextDecoder("utf-8");
        const reader = file.stream().getReader({ mode: "byob" });

        while (true) {
            const buffer = new Uint8Array(new ArrayBuffer(bufferSize));
            const data = await reader.read(buffer);

            if (data.done) break;

            const text = `${++index}${decoder.decode(data.value)}`;
            console.log(text);

            const el = qrCodeWriter.write(text, 320, 240);

            qrCodeArea.removeChild(qrCodeArea.firstChild!);

            qrCodeArea.appendChild(el);

            await delay(200);
        }
    }
</script>

<div>
    <input bind:files type="file" style="display: block;" />

    <div>
        <input
            min="16"
            max="1024"
            step="8"
            bind:value={bufferSize}
            type="number"
        />
        <input
            bind:value={bufferSize}
            step="16"
            type="range"
            min="8"
            max="1024"
        />
    </div>

    <div bind:this={qrCodeArea}><p></p></div>
</div>
