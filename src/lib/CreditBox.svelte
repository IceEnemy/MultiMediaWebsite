<script>
    export let name;
    export let roles;
    export let image;
</script>

<div class="creditContainer">
    <img src={image} alt={name} />
    <div class="nameContainer">
        <span class="name">{name}</span>
    </div>
    <div class="roleContainer">
        {#each roles as role}
            <span class="roles">{role}</span>
        {/each}
    </div>
    
</div>

<style>
    .roleContainer{
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        margin-top: 1rem;
        gap: 10px;;
    }
    .nameContainer {
        height: 80px;
        display: flex;
        align-items: center;
        justify-content: center;
        color: white;
    }

    .name {
        font-weight: bold;
        font-size: 1.5rem;
        text-align: center;
    }

    .creditContainer {
        display: flex;
        flex-direction: column;
        overflow: hidden;
        width: 280px;
        height: 350px;
        background-color: rgb(36, 35, 36);
        padding: 10px;
        transition: height 0.2s, color 0.2s;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
    }

    .creditContainer img {
        width: 280px;
        height: 280px;
        object-fit: cover;
        border-radius: 10px;
        transition: none;
    }

    .creditContainer:hover {
        height: 500px;
    }

    .roles {
        color: transparent;
        transition: color 0.2s;
        font-size: 1.5rem;
        
    }

    .creditContainer:hover .roles {
        color: white;
    }
</style>
