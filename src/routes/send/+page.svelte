<script lang="ts">
    import { BrowserQRCodeSvgWriter } from "@zxing/browser";

    const qrCodeWriter = new BrowserQRCodeSvgWriter();

    let files: FileList | null | undefined = $state();

    let svg: SVGSVGElement;

    $effect(() => {
        if (files) {
            const file = files.item(0);
            if (file) writeFile(file);
        }
    });

    async function writeFile(file: File) {
        const el = qrCodeWriter.write(await file.text(), 320, 240);
        svg.outerHTML = el.outerHTML;
    }
</script>

<div>
    <input bind:files type="file" style="display: block;" />

    <svg bind:this={svg} />
</div>
