<script>
    import { onMount } from "svelte";
    import global from "../Images/global.png";
    import music from "../Images/music-note.png";
    import masks from "../Images/masks.png";
    import plane from "../Images/plane.png";

    let articles = [];
    let isLoading = true;

    onMount(async () => {
        try {
            const response = await fetch(
                "https://newsapi.org/v2/top-headlines?country=us&apiKey=9a143e52ce394c398544c09e2bfe2df4"
            );
            const data = await response.json();
            articles = data.articles.slice(1, 4);
            isLoading = false; // Set isLoading to false once data is fetched
        } catch (error) {
            console.error(error);
        }
    });
</script>

<!-- can be called from exernal api component-->

<!-- fix loading spinner bug-->
<h1 class="makeBorder">The Latest News</h1>
<div class="threeBoxes">
    {#if isLoading}
        <div class="lds-dual-ring" />
        <!-- Display loading spinner -->
    {:else}
        {#each articles as article}
            <article class="theArticle">
                <h2 class="articleTitle">{article.title}</h2>
                <!--5 maybe link to seperate article page-->
                {#if article.urlToImage}
                    <img
                        class="fixSize"
                        src={article.urlToImage}
                        alt={article.title}
                    />
                {:else}
                    <div class="lds-dual-ring" />
                    <!-- Display loading spinner for individual articles without image -->
                {/if}
            </article>
        {/each}
    {/if}
</div>

<div class="theBanner">
    <h2 class="styleTheF">Join The Forum today</h2>
</div>

<!-- Pull data from seperate pages - then link them, and also display content on home page-->
<div class="theIcons">
    <div class="fourBoxes">
        <div class="globalNews">
            <img src={global} alt="global news" />
            <h4 class="newsMD">Global News</h4>
        </div>
        <div class="globalNews">
            <img src={music} alt="music note" />
            <h4 class="newsMD">Music</h4>
        </div>
        <div class="globalNews">
            <img src={masks} alt="culture" />
            <h4 class="newsMD">Culture</h4>
        </div>
        <div class="globalNews">
            <img src={plane} alt="travel" />
            <h4 class="newsMD">Travel</h4>
        </div>
    </div>
</div>

<style>
    /*seperate the boxes - like services pages */
    .fourBoxes {
        margin-top: 40px !important;
        display: flex;
        flex-direction: row;
        place-content: center !important;
        justify-content: space-between !important;
        width: 60%;
        margin: 0 auto;
        /* sort out height issue */
    }

    .newsMD {
        margin-top: 10px;
    }

    .globalNews {
        padding: 20px;
        background-color: #f2f2f2;
        border: 1px solid rgb(69, 66, 66);
        width: 24.9% !important;
        margin: 0 auto;
        text-align: center;
    }

    .theIcons {
    }
    .styleTheF {
        color: #ffffff;
        font-size: 30px;
        padding-top: 12px;
        font-family: "Guardian Egyptian Web", Georgia, serif;
    }
    .theBanner {
        background-color: rgb(166, 22, 22);
        box-shadow: 0px 5px 14px 2px rgba(0, 0, 0, 0.58);
        height: 65px;
        width: 82%;
        margin: 0 auto;
    }

    .fixSize {
        max-width: 100%;
    }
    .articleTitle {
        font-size: 16px !important;
    }

    h2 {
        text-align: center;
    }

    .homeTitle {
        text-align: center;
    }

    .threeBoxes {
        display: flex;
        justify-content: center;
        /* sort out height issue */
    }

    .theArticle {
        margin-top: 20px;
        padding-top: 20px;
        border: 1px solid rgb(138, 135, 135, 0.2);
        width: 26% !important;
        margin-bottom: 50px;
        margin: 20px;
    }

    .articleTitle {
        padding: 10px;
        font-size: 14px;
        text-align: left;
    }

    .lds-dual-ring {
        margin: 0 auto;
        margin-top: 50px;
        display: inline-block;
        width: 90px;
        height: 90px;
        background-color: rgb(212, 207, 207);
        border-radius: 50px;
        margin-bottom: 50px;
    }
    .lds-dual-ring:after {
        content: " ";
        display: block;
        width: 64px;
        height: 64px;
        margin: 8px;
        border-radius: 50%;
        border: 6px solid #fff;
        border-color: #fff transparent #fff transparent;
        animation: lds-dual-ring 1.2s linear infinite;
    }
    @keyframes lds-dual-ring {
        0% {
            transform: rotate(0deg);
        }
        100% {
            transform: rotate(360deg);
        }
    }

    @media screen and (max-width: 765px) {
        .threeBoxes {
            flex-direction: column;
        }

        .theArticle {
            width: 50% !important;
            margin: 0 auto;
            padding: 20px;
            margin-top: 20px;
            margin-bottom: 20px;
        }

        .fourBoxes {
            flex-direction: column;
        }

        .globalNews {
            width: 100% !important;
        }
    }
</style>
