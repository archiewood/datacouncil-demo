# Hey {#if $page.query.get("name")} {$page.query.get("name")}{:else} there{/if}!

Hope you are enjoying Data Council!

{#if $page.query.get("name")}

This report was generated just for you at {new Date().toLocaleString()}

{/if}

