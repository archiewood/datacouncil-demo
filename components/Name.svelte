<script>
    let name=null
    import {browser} from "$app/environment";
    import {page} from "$app/stores";
    const searchParams = browser && $page.url.searchParams
 
    if (searchParams && searchParams.get("name")) {
        name = searchParams.get("name")
        }
</script>


{#if name}<span>{name}</span>{/if}