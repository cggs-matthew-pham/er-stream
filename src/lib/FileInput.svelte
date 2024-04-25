<script lang="ts">
export let accept: string = '.pdf';
export let onFileSelect: (file: File) => void;

function handleFileChange(event: Event) {
    const input = event.target as HTMLInputElement;
    if (input.files?.length) {
        onFileSelect(input.files[0]);
    }
}
</script>

<input type="file" {accept} on:change={handleFileChange} />
