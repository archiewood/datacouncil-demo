<script>
    let name=null
    import {page} from "$app/stores";

    if ($page.query.get("name")) {        
        name = $page.query.get("name")
    }
</script>


{#if name}<span>{name}</span>{/if}