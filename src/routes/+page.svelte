<script>
    import CreditBox from '$lib/CreditBox.svelte';
    import { goto } from '$app/navigation';
    import gerSelfPhoto from '$lib/assets/gerSelfPhoto.jpg';
    import belleSelfPhoto from '$lib/assets/belleSelfPhoto.jpg';
    import celSelfPhoto from '$lib/assets/celSelfPhoto.jpg';
    import norSelfPhoto from '$lib/assets/norSelfPhoto.jpg';
    import raymSelfPhoto from '$lib/assets/raymSelfPhoto.jpg';
    import mulmedTrailer from '$lib/assets/Mulmed_trailer.mov';
    import { base } from '$app/paths';


    let credits = [
        {
            name: "Julius Gerald Pho",
            roles: ["Scriptwriter", "Cameraman"],
            image: gerSelfPhoto
        },
        {
            name: "Ignatia Christabelle Amadea Hardjono",
            roles: ["Scriptwriter", "Video Editor", "Main Actress"],
            image: belleSelfPhoto
        },
        {
            name: "Celina Chintya",
            roles: ["Scriptwriter", "Actress (Chef on TV)"],
            image: celSelfPhoto
        },
        {
            name: "Norberth Erlin Putra",
            roles: ["Scriptwriter", "Prop Provider", "Website Developer"],
            image: norSelfPhoto
        },
        {
            name: "Raymond Willy Tanumihardja",
            roles: ["Prop Provider", "Main Actor"],
            image: raymSelfPhoto
        }
    ];

    let isMuted = true;

    function playVideo() {
        const video = document.querySelector('.trailerVideo');
        video.play();
    }

    function pauseVideo() {
        const video = document.querySelector('.trailerVideo');
        video.pause();
    }

    function toggleMute() {
        const video = document.querySelector('.trailerVideo');
        isMuted = !isMuted;
        video.muted = isMuted;
    }

    function watchVideo() {
        goto(`${base}/videoPlayer`);
    }
</script>

<!-- svelte-ignore a11y-no-static-element-interactions -->
<div class="movieTrailer" on:mouseenter="{playVideo}" on:mouseleave="{pauseVideo}">
    <div class="gradientFade"></div>

    <div class="textContainer">
        <span class="ingrid-darling-title">Meals on a Dime</span>
    </div>

    <div class="synopsisContainer">
        <span>Two Apartmates, Raymond and Belle realize their takeout habit is costly, leading Belle to embrace cooking while Raymond sticks to his routine. When Raymond struggles to afford an end-of-semester trip, Belle convinces them to cook together, saving money and strengthening their friendship in the process.</span>
    </div>
    <div class="buttons">
        <button class="playButton" on:click={watchVideo}><span class="ph--play-fill"></span>
            Watch Movie
        </button>

        <button class="audioButton" on:click="{toggleMute}">
            <span class="{isMuted ? "octicon--mute-16" : "octicon--unmute-16"}"></span>
        </button>
    </div>
    <video class="trailerVideo" src={mulmedTrailer} muted loop autoplay></video>
</div>

<div class="credits">
    <h1>Credits</h1>

    <div class="creditContent">
        {#each credits as credit}
            <CreditBox name={credit.name} roles={credit.roles} image={credit.image} />
        {/each}
    </div>
</div>

<style>

    .buttons {
        z-index: 2;
        display: flex;
        flex-direction: row;
        justify-content: space-between;
    }

    .creditContent {
        display: flex;
        flex-wrap: wrap;
        gap: 10px;
        justify-content: center;
    }

    h1 {
        margin: 20px;
        font-size: 3.5rem;
        justify-self: center;
    }

    .gradientFade {
        width: 100%;
        height: 400px;
        background: linear-gradient(4deg, var(--dark) 0%, transparent 70%, transparent 100%);
        position: absolute;
        z-index: 0;
        left: 0;
        bottom: 0;
    }

    .playButton {
        width: fit-content;
        height: 2.5rem;
        background-color: white;
        border: none;
        border-radius: 10px;
        z-index: 1;
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 5px;
        font-size: 1rem;
    }

    .playButton:hover {
        background-color: var(--orange);
        color: white;
        transition: 0.2s;
    }

    .textContainer {
        width: fit-content;
        color: white;
        z-index: 1;
    }

    .synopsisContainer {
        width: 450px;
        color: white;
        z-index: 1;
    }

    .movieTrailer {
        width: calc(100% - 40px);
        background: url('$lib/assets/ThumbnailImg.jpg') no-repeat center center;
        background-size: cover;
        height: calc(100vh - 40px);
        margin: 0;
        gap: 20px;
        display: flex;
        flex-direction: column;
        justify-content: end;
        padding: 20px;
        position: relative;
    }

    .movieTrailer .trailerVideo {
        display: none;
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        object-fit: cover;
        z-index: 0;
    }

    .movieTrailer:hover .trailerVideo {
        display: block;
    }

    .movieTrailer:hover {
        background: none;
    }

    .credits {
        color: white;
        display: flex;
        flex-direction: column;
        align-items: center;
        width: 100%;
        min-height: 70vh;
        background-color: var(--dark);
        margin: 0;
    }

    .ph--play-fill, .ph--volume-high-fill {
        display: inline-block;
        width: 1em;
        height: 1em;
        --svg: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 256 256'%3E%3Cpath fill='%23000' d='M240 128a15.74 15.74 0 0 1-7.6 13.51L88.32 229.65a16 16 0 0 1-16.2.3A15.86 15.86 0 0 1 64 216.13V39.87a15.86 15.86 0 0 1 8.12-13.82a16 16 0 0 1 16.2.3l144.08 88.14A15.74 15.74 0 0 1 240 128'/%3E%3C/svg%3E");
        background-color: currentColor;
        -webkit-mask-image: var(--svg);
        mask-image: var(--svg);
        -webkit-mask-repeat: no-repeat;
        mask-repeat: no-repeat;
        -webkit-mask-size: 100% 100%;
        mask-size: 100% 100%;
    }

    .ingrid-darling-title {
        font-family: "Ingrid Darling", cursive;
        font-weight: 400;
        font-style: normal;
        font-size: 100px;
    }

    .audioButton {
        font-size: 1rem;
        width: 40px;
        height: 40px;
        background-color: white;
        border: none;
        border-radius: 50%;
        display: flex;
        justify-content: center;
        align-items: center;
        cursor: pointer;
        z-index: 1;
    }

    .audioButton:hover {
        background-color: var(--orange);
        color: white;
        transition: 0.2s;
    }

    .octicon--mute-16 {
        display: inline-block;
        width: 1em;
        height: 1em;
        --svg: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 16 16'%3E%3Cpath fill='%23000' d='M8 2.75v10.5a.751.751 0 0 1-1.238.57L3.473 11H1.75A1.75 1.75 0 0 1 0 9.25v-2.5C0 5.784.784 5 1.75 5h1.722l3.29-2.82A.75.75 0 0 1 8 2.75m3.28 2.47L13 6.94l1.72-1.72a.75.75 0 0 1 1.042.018a.75.75 0 0 1 .018 1.042L14.06 8l1.72 1.72a.749.749 0 0 1-.326 1.275a.75.75 0 0 1-.734-.215L13 9.06l-1.72 1.72a.749.749 0 0 1-1.275-.326a.75.75 0 0 1 .215-.734L11.94 8l-1.72-1.72a.749.749 0 0 1 .326-1.275a.75.75 0 0 1 .734.215m-7.042 1.1a.75.75 0 0 1-.488.18h-2a.25.25 0 0 0-.25.25v2.5c0 .138.112.25.25.25h2c.179 0 .352.064.488.18L6.5 11.62V4.38Z'/%3E%3C/svg%3E");
        background-color: currentColor;
        -webkit-mask-image: var(--svg);
        mask-image: var(--svg);
        -webkit-mask-repeat: no-repeat;
        mask-repeat: no-repeat;
        -webkit-mask-size: 100% 100%;
        mask-size: 100% 100%;
    }

    .octicon--unmute-16 {
        display: inline-block;
        width: 1em;
        height: 1em;
        --svg: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 16 16'%3E%3Cpath fill='%23000' d='M7.563 2.069A.75.75 0 0 1 8 2.75v10.5a.751.751 0 0 1-1.238.57L3.472 11H1.75A1.75 1.75 0 0 1 0 9.25v-2.5C0 5.784.784 5 1.75 5h1.723l3.289-2.82a.75.75 0 0 1 .801-.111M6.5 4.38L4.238 6.319a.75.75 0 0 1-.488.181h-2a.25.25 0 0 0-.25.25v2.5c0 .138.112.25.25.25h2c.179 0 .352.064.488.18L6.5 11.62Zm6.096-2.038a.75.75 0 0 1 1.06 0a8 8 0 0 1 0 11.314a.75.75 0 0 1-1.042-.018a.75.75 0 0 1-.018-1.042a6.5 6.5 0 0 0 0-9.193a.75.75 0 0 1 0-1.06Zm-1.06 2.121l-.001.001a5 5 0 0 1 0 7.07a.749.749 0 0 1-1.275-.326a.75.75 0 0 1 .215-.734a3.5 3.5 0 0 0 0-4.95a.75.75 0 1 1 1.061-1.061'/%3E%3C/svg%3E");
        background-color: currentColor;
        -webkit-mask-image: var(--svg);
        mask-image: var(--svg);
        -webkit-mask-repeat: no-repeat;
        mask-repeat: no-repeat;
        -webkit-mask-size: 100% 100%;
        mask-size: 100% 100%;
    }
</style>
