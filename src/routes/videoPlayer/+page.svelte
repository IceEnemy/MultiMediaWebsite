<script>
    import { goto } from '$app/navigation';
    import { page } from '$app/stores';

    function goBack() {
        // Navigate back to the previous page
        const currentUrl = $page.path ? $page.path : '';

        if (!currentUrl) {
            goto('/');
        }
        else{
            goto('/');
        }

        
    }
</script>

<div class="videoContainer">
    <button class="backButton" on:click="{goBack}">Back</button>
    <iframe 
        class="videoElement" 
        width="100%" 
        height="100%" 
        src="https://www.youtube.com/embed/IoPgEDTabU0" 
        frameborder="0" 
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" 
        allowfullscreen>
    </iframe>
</div>

<style>
    .videoContainer {
        position: relative;
        display: flex;
        justify-content: center;
        align-items: center;
        width: 100%;
        height: 100vh;
        padding: 0;
        margin: 0;
        background-color: #15191e;
    }

    .backButton {
        position: absolute;
        top: 20px;
        left: 20px;
        background-color: white;
        border: none;
        padding: 10px 20px;
        border-radius: 5px;
        cursor: pointer;
        font-size: 1rem;
        z-index: 2;
    }

    .backButton:hover {
        background-color: #a5633d;
        color: white;
    }

    .videoElement {
        width: 80%;
        height: 80%;
    }
</style>
