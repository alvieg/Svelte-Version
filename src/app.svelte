<script>
    let url = '';
    let modalOpen = false;
    let modalUrl = '';
    let isLight = false;
    let iframeEl;

    const gameButtons = {
        "GHUB": "https://thegportal.neocities.org",
        "Burger Awesome": "https://burgerawesome.neocities.org",
        "HaHa Games": "https://hahagames.com",
        "Butter Dog Games": "https://teachers-are-the-best.neocities.org",
        "GN-Math": "https://gn-math.github.io",
        "MiniPlay": "https://miniplay.com",
        "GHUB V2": "https://v2.thegportal.net",
        "Space (Proxy)": "https://gointospace.app",
        "3KH0": "https://3kh0s.github.io",
        "Games 4 Free": "https://games-4-free.com",
        "Proxy (WIP)": "https://gameportal-v3-2025.vercel.app/proxy.html",
        "Interstellar": "https://interstellar-2025.vercel.app/",
    };

    function openModal(URL) {
        modalUrl = URL;
        modalOpen = true;
        url = '';
    }

    function closeModal() {
        modalOpen = false;
        modalUrl = '';
    }

    function toggleTheme() {
        isLight = !isLight;
    }

    function openInNewTab(URL) {
        const win = window.open();
        win.document.write(`<embed src="${URL}" frameborder="0" style="width:100vw;height:100vh;border:none;">`);
        win.document.title = "About:Blank Game";
    }

    function redirect() {
        openInNewTab(modalUrl);
    }

    function fullscreenIframe() {
        if (iframeEl && iframeEl.requestFullscreen) {
            iframeEl.requestFullscreen();
        }
    }
</script>

<main class:light={isLight}>
    <div class="title">
        <h1>Click a button to open in PopUp</h1>
        <h2 class="sectionTitle">Click alt escape or click out to close the PopUp</h2>
        <button type="button" class="toggle" on:click={toggleTheme}>Toggle Light/Dark</button>
        <button type="button" class="toggle" on:click={() => openInNewTab('https://gameportal-v3-2025.vercel.app/')}>Open in About:Blank</button>
    </div>

    <div class="buttonSpace">
        {#each Object.entries(gameButtons) as [key, value]}
            <button type="button" class="gameButton" on:click={() => openModal(value)}>{key}</button>
        {/each}
    </div>

    <br><br>
    <br><br>

    <div class="proxy">
        <input
            type="url"
            placeholder="https://example.com"
            class="inputBox"
            bind:value={url}
            on:keydown={(e) => { if (e.key === 'Enter') openModal(url); }}
        >
        <button type="button" class="urlButton" on:click={() => openModal(url)}>Go!</button>
    </div>

    {#if modalOpen}
        <div class="modal-overlay" on:click={closeModal}></div>
        <div class="modal">
            <div class="modalToolbar">
                <button type="button" class="modalToolbarBtn closeModalBtn" on:click={closeModal}>Close</button>
                <button type="button" class="modalToolbarBtn FsBtn" on:click={fullscreenIframe}>Fullscreen</button>
                <button type="button" class="modalToolbarBtn AbtBlnkBtn" on:click={redirect}>Open In About:Blank</button>
            </div>
            <embed bind:this={iframeEl} class="iframe" src={modalUrl}>
        </div>
    {/if}
</main>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@500&display=swap');

    :root {
        --button-color: dodgerblue;
        --txt-color: white;
        --bg-color: black;
        --button-txt-color: white;
        --btn-hover-bg-clr: black;
    }

    .light {
        --button-color: dodgerblue;
        --txt-color: dodgerblue;
        --bg-color: white;
        --btn-hover-bg-clr: white;
        --button-txt-color: black;
        animation: darkToLight 3s;
    }

    * {
        font-family: 'Orbitron', sans-serif;
        cursor: url('pizza.gif');
        animation: fadeIn 3s;
        box-sizing: border-box;
    }

    @keyframes fadeIn {
        from { opacity: 0; }
        to { opacity: 1; }
    }

    @keyframes darkToLight {
        from { background-color: black; }
        to { background-color: white; }
    }

    @keyframes lightToDark {
        from { background-color: white; }
        to { background-color: black; }
    }

    main {
        background-color: var(--bg-color);
        color: var(--txt-color);
        min-height: 100vh;
        width: 100vw;
        margin: 0;
        display: flex;
        flex-direction: column;
        align-items: stretch;
        transition: background-color 0.3s;
    }

    .title {
        text-align: center;
        color: var(--txt-color);
        font-size: 48px;
        margin-bottom: 1.5rem;
    }

    .sectionTitle {
        font-size: 24px;
        color: var(--txt-color);
    }

    .buttonSpace {
        display: flex;
        flex-wrap: wrap;
        gap: 1rem;
        justify-content: center;
        margin-bottom: 2rem;
    }

    .gameButton {
        background-color: var(--button-color);
        color: var(--button-txt-color);
        border: 5px solid dodgerblue;
        border-radius: 8px;
        cursor: pointer;
        font-size: 2rem;
        text-align: center;
        margin: 1%;
        width: 48%;
        height: 15vh;
        transition: transform 0.3s, box-shadow 0.3s;
    }

    .gameButton:hover {
        background-color: var(--btn-hover-bg-clr);
        color: dodgerblue;
    }

    .toggle,
    .urlButton,
    .modalToolbarBtn {
        cursor: pointer;
        background-color: var(--button-color);
        color: var(--button-txt-color);
        border: 2px solid dodgerblue;
        border-radius: 8px;
        text-align: center;
        font-size: 1rem;
        margin: 1vh;
        width: 10vw;
        height: 5vh;
        transition: transform 0.3s, border-radius 0.5s;
    }

    .toggle:hover,
    .urlButton:hover {
        background-color: var(--btn-hover-bg-clr);
        border-radius: 30px;
        color: dodgerblue;
        transform: scale(1.025);
    }

    .proxy {
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 1rem;
        margin-bottom: 2rem;
    }

    .inputBox {
        padding: 13px;
        border: 2px solid dodgerblue;
        border-radius: 5px;
        font-size: 16px;
        width: 25%;
    }

    .inputBox::placeholder {
        color: #888;
        font-style: italic;
    }

    .modal-overlay {
        display: block;
        position: fixed;
        top: 0;
        left: 0;
        width: 100vw;
        height: 100vh;
        background-color: rgba(0, 0, 0, 0.5);
        z-index: 998;
    }

    .modal {
        display: block;
        position: fixed;
        top: 50%;
        left: 50%;
        height: 100%;
        width: 100%;
        transform: translate(-50%, -50%);
        background-color: var(--bg-color);
        padding: 0;
        border: none;
        border-radius: 0;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        z-index: 999;
        overflow: hidden;
    }

    .modalToolbar {
        display: flex;
        background-color: gray;
        justify-content: space-evenly;
        align-items: center;
        height: 5%;
        width: 100%;
        position: absolute;
        top: 0;
        left: 0;
        z-index: 1000;
    }

    .iframe {
        height: 95%;
        width: 100%;
        margin: 0;
        border: none;
        border-radius: 8px;
        overflow: hidden;
        z-index: 1000;
    }
</style>
