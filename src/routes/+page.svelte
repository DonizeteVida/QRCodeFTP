<script lang="ts">
    import { resolve } from "$app/paths";
</script>

<a class="btn btn-blue" href={resolve("/send")}>Send file</a>
<a class="btn btn-blue" href={resolve("/receive")}>Receive a file</a>

<style lang="postcss">
    @reference "tailwindcss";

    .btn {
        @apply font-bold py-2 px-4;
    }
    .btn-blue {
        @apply bg-blue-500 text-white;
    }
    .btn-blue:hover {
        @apply bg-blue-700;
    }
</style>
