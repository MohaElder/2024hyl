<script lang="ts">
    import { writable } from "svelte/store";
    import Card from "../lib/Card.svelte";
    import type { Card as CardType } from "../lib/types";
    import { fade } from "svelte/transition";

    let cards: CardType[] = [
        {
            id: 1,
            imgUrl: "/src/assets/15.jpeg",
            text: "在我们开始前，请保证你不会生气",
            swipeLeft: { cardId: 3, transitionText: "好的，我不生气" },
            swipeRight: { cardId: 2, transitionText: "那可不行" },
        },
        {
            id: 2,
            imgUrl: "/src/assets/15.jpeg",
            text: "在我们开始前，请保证你不会生气",
            swipeLeft: { cardId: 3, transitionText: "好的，我不生气" },
            swipeRight: { cardId: 1, transitionText: "那可不行" },
        },
        {
            id: 3,
            imgUrl: "/src/assets/35.jpeg",
            text: "Let's vc",
            swipeLeft: { cardId: 4, transitionText: "你今天咋样" },
            swipeRight: { cardId: 4, transitionText: "最近咋样" },
        },
        {
            id: 4,
            imgUrl: "/src/assets/27.jpeg",
            text: "我还不错，你呢？",
            swipeLeft: { cardId: 5, transitionText: "还好，最近有点累" },
            swipeRight: { cardId: 6, transitionText: "你能不能不要截图了" },
        },
        {
            id: 5,
            imgUrl: "/src/assets/26.jpeg",
            text: "我最近也挺忙的，但很开心，你开心不",
            swipeLeft: { cardId: 7, transitionText: "不开心" },
            swipeRight: { cardId: 8, transitionText: "开心" },
        },
        {
            id: 6,
            imgUrl: "/src/assets/26.jpeg",
            text: "ok！",
            swipeLeft: { cardId: 5, transitionText: "。。。" },
            swipeRight: { cardId: 5, transitionText: "额" },
        },
        {
            id: 7,
            imgUrl: "/src/assets/28.jpeg",
            text: "那先不和你聊啦，你去做点开心的事情～",
            swipeLeft: { cardId: 9, transitionText: "好滴" },
            swipeRight: { cardId: 3, transitionText: "再聊一会儿吧" },
        },
        {
            id: 8,
            imgUrl: "/src/assets/35.jpeg",
            text: "那就好～那我先走啦",
            swipeLeft: { cardId: 9, transitionText: "好滴" },
            swipeRight: { cardId: 3, transitionText: "再聊一会儿吧" },
        },
        {
            id: 9,
            imgUrl: "/src/assets/23.jpeg",
            text: "You're waiting for a train. A train that will take you far away. You know where you hope this train will take you, but you don't know for sure. But it doesn't matter, because we'll be together.",
            swipeLeft: { cardId: 10, transitionText: "Take me to church" },
            swipeRight: { cardId: 11, transitionText: "Take me home" },
        },
        {
            id: 10,
            imgUrl: "/src/assets/4.jpeg",
            text: "You're at the City upon a Hill",
            swipeLeft: { cardId: 12, transitionText: "我每天爬山确实挺累的" },
            swipeRight: { cardId: 11, transitionText: "I want to escape" },
        },
        {
            id: 12,
            imgUrl: "/src/assets/24.jpeg",
            text: "至少这个城市挺可爱的～",
            swipeLeft: { cardId: 13, transitionText: "Yea！" },
            swipeRight: { cardId: 13, transitionText: "hhh" },
        },
        {
            id: 13,
            imgUrl: "/src/assets/22.jpeg",
            text: "而且人也很可爱",
            swipeLeft: { cardId: 14, transitionText: "Awww" },
            swipeRight: {
                cardId: 14,
                transitionText: "这不是Providence吧。。。",
            },
        },
        {
            id: 14,
            imgUrl: "/src/assets/25.jpeg",
            text: "城市也挺漂亮滴",
            swipeLeft: { cardId: 15, transitionText: "I think it's Boston" },
            swipeRight: { cardId: 9, transitionText: "I love South Bay~" },
        },
        {
            id: 15,
            imgUrl: "/src/assets/11.jpeg",
            text: "How many more times will you watch the full moon rise? Perhaps twenty, and yet it all seems limitless",
            swipeLeft: {
                cardId: 16,
                transitionText: "Perhaps four or five times more",
            },
            swipeRight: { cardId: 16, transitionText: "Perhaps not even that" },
        },
        {
            id: 16,
            imgUrl: "/src/assets/10.jpeg",
            text: "你会想起多少次童年中，某个特定的下午，某个深深成为你生命一部分的下午，如果没有它，你甚至无法想象自己的人生",
            swipeLeft: { cardId: 11, transitionText: "也许，四或五次吧" },
            swipeRight: { cardId: 9, transitionText: "没想过" },
        },
        {
            id: 11,
            imgUrl: "/src/assets/29.jpeg",
            text: "12 Bar Blues不错吧",
            swipeLeft: { cardId: 17, transitionText: "蛮好的" },
            swipeRight: {
                cardId: 17,
                transitionText: "我觉得调酒师蛮好看的。。。",
            },
        },
        {
            id: 17,
            imgUrl: "/src/assets/30.jpeg",
            text: "帮你拍张照片",
            swipeLeft: { cardId: 18, transitionText: "ok" },
            swipeRight: { cardId: 18, transitionText: "。。。" },
        },
        {
            id: 18,
            imgUrl: "/src/assets/36.jpeg",
            text: "也许我们见不到满月升起，但我们见到满月的一举一动也许会成为其他人的数次满月升起",
            swipeLeft: { cardId: 19, transitionText: "希望能再次见到满月升起" },
            swipeRight: { cardId: 19, transitionText: "Earth is flat" },
        },
        {
            id: 19,
            imgUrl: "/src/assets/10.jpeg",
            text: "Now we're back",
            swipeLeft: {
                cardId: 20,
                transitionText: "And I guess nothing has changed",
            },
            swipeRight: {
                cardId: 14,
                transitionText: "I'm feeling different now",
            },
        },
        {
            id: 20,
            imgUrl: "/src/assets/15.jpeg",
            text: "Now I'm back",
            swipeLeft: { cardId: 21, transitionText: "Ok!" },
            swipeRight: { cardId: 21, transitionText: "我要吃蛋饼" },
        },
        {
            id: 21,
            imgUrl: "/src/assets/3.jpeg",
            text: "我来做饭",
            swipeLeft: { cardId: 22, transitionText: "我来洗碗" },
            swipeRight: { cardId: 22, transitionText: "好滴" },
        },
        {
            id: 22,
            imgUrl: "/src/assets/2.jpeg",
            text: "做好啦",
            swipeLeft: { cardId: 23, transitionText: "wow！" },
            swipeRight: { cardId: 23, transitionText: "看上去好好吃" },
        },
        {
            id: 23,
            imgUrl: "/src/assets/32.jpeg",
            text: "你拍吧",
            swipeLeft: { cardId: 24, transitionText: "。。。" },
            swipeRight: { cardId: 24, transitionText: "ok" },
        },
        {
            id: 24,
            imgUrl: "/src/assets/33.jpeg",
            text: "开动咯",
            swipeLeft: { cardId: 25, transitionText: "yidadakimasu" },
            swipeRight: { cardId: 25, transitionText: "yay！" },
        },
        {
            id: 25,
            imgUrl: "/src/assets/31.jpeg",
            text: "今天风好大",
            swipeLeft: { cardId: 26, transitionText: "我快要被吹飞了" },
            swipeRight: { cardId: 26, transitionText: "我差点被吹飞了" },
        },
        {
            id: 26,
            imgUrl: "/src/assets/23.jpeg",
            text: "坐火车去吧",
            swipeLeft: { cardId: 28, transitionText: "Is it a dejavu？" },
            swipeRight: { cardId: 27, transitionText: "Am I on the train？" },
        },
        {
            id: 27,
            imgUrl: "/src/assets/21.jpeg",
            text: "我们在太空",
            swipeLeft: { cardId: 29, transitionText: "在太空看得到满月升起吗" },
            swipeRight: { cardId: 28, transitionText: "cool" },
        },
        {
            id: 28,
            imgUrl: "/src/assets/20.jpeg",
            text: "满月在太空不会升起，但是我们的影子也许能看到他升起",
            swipeLeft: { cardId: 27, transitionText: "ok" },
            swipeRight: { cardId: 27, transitionText: "ok" },
        },
        {
            id: 29,
            imgUrl: "/src/assets/15.jpeg",
            text: "我很高，你很矮",
            swipeLeft: { cardId: 30, transitionText: "sb" },
            swipeRight: { cardId: 30, transitionText: "That's right!" },
        },
        {
            id: 30,
            imgUrl: "/src/assets/15.jpeg",
            text: "拍张合照吧！",
            swipeLeft: { cardId: 31, transitionText: "？" },
            swipeRight: { cardId: 33, transitionText: "就这样吧" },
        },
        {
            id: 31,
            imgUrl: "/src/assets/15.jpeg",
            text: "拍张合照吧！",
            swipeLeft: { cardId: 32, transitionText: "？" },
            swipeRight: { cardId: 33, transitionText: "就这样吧" },
        },
        {
            id: 32,
            imgUrl: "/src/assets/15.jpeg",
            text: "拍张合照吧！",
            swipeLeft: { cardId: 30, transitionText: "？" },
            swipeRight: { cardId: 33, transitionText: "就这样吧" },
        },
        {
            id: 33,
            imgUrl: "/src/assets/5.jpeg",
            text: "再拍一张！",
            swipeLeft: { cardId: 34, transitionText: "？" },
            swipeRight: { cardId: 38, transitionText: "就这样吧" },
        },
        {
            id: 34,
            imgUrl: "/src/assets/6.jpeg",
            text: "再拍一张！",
            swipeLeft: { cardId: 35, transitionText: "？" },
            swipeRight: { cardId: 38, transitionText: "就这样吧" },
        },
        {
            id: 35,
            imgUrl: "/src/assets/7.jpeg",
            text: "再拍一张！",
            swipeLeft: { cardId: 36, transitionText: "？" },
            swipeRight: { cardId: 38, transitionText: "就这样吧" },
        },
        {
            id: 36,
            imgUrl: "/src/assets/8.jpeg",
            text: "再拍一张！",
            swipeLeft: { cardId: 37, transitionText: "？" },
            swipeRight: { cardId: 38, transitionText: "就这样吧" },
        },
        {
            id: 37,
            imgUrl: "/src/assets/9.jpeg",
            text: "再拍一张！",
            swipeLeft: { cardId: 34, transitionText: "？" },
            swipeRight: { cardId: 38, transitionText: "就这样吧" },
        },
        {
            id: 38,
            imgUrl: "/src/assets/13.jpeg",
            text: "吃点东西休息一下",
            swipeLeft: { cardId: 39, transitionText: "好吃捏" },
            swipeRight: { cardId: 39, transitionText: "不要再拍我了" },
        },
        {
            id: 39,
            imgUrl: "/src/assets/14.jpeg",
            text: "再吃个晚饭",
            swipeLeft: { cardId: 40, transitionText: "好吃" },
            swipeRight: { cardId: 40, transitionText: "吃不下了。。。" },
        },
        {
            id: 40,
            imgUrl: "/src/assets/34.jpeg",
            text: "晚饭吃完了，我走咯",
            swipeLeft: { cardId: 100, transitionText: "Au Revoir" },
            swipeRight: { cardId: 1, transitionText: "舍不得你" },
        },
    ];
    let currentCardIndex = writable(0);

    $: currentCard =
        $currentCardIndex < cards.length ? cards[$currentCardIndex] : null;

    let backgroundDiv: HTMLDivElement;

    function handleSwipe(direction: string): void {
        let idx = currentCard?.swipeLeft?.cardId;
        if (direction === "right") {
            idx = currentCard!.swipeRight.cardId;
        }
        if (idx! <= cards.length) {
            currentCardIndex.update((n) => {
                const card = cards.find((card) => card.id === idx);
                if (card) {
                    n = cards.indexOf(card);
                }
                return n;
            });
        } else {
            // Handle the end of the cards array, maybe reset or show a message
            if (direction === "right") {
                backgroundDiv.classList.add("bg-green");
                backgroundDiv.classList.add("background-transition");
            } else {
                backgroundDiv.classList.add("bg-yellow");
                backgroundDiv.classList.add("background-transition");
            }
            currentCard = null;
        }
    }
</script>

<div class="full-screen" bind:this={backgroundDiv}>
    <div class="container">
        {#if currentCard}
            <!-- Use the card's id (or index) as a key to reset component state -->
            {#key currentCard.id}
                <div transition:fade={{ duration: 300 }}>
                    <Card card={currentCard} onSwipe={handleSwipe} />
                </div>
            {/key}
        {:else}
            <p>
               That's it! 生日快乐～你敢相信吗，这是我们认识的第6还是第7年了，而我们才20出头。我以前常觉得6/7年的交情应该属于三四十岁才有的。但我后面想想，三四十岁才交到6/7年的朋友其实没什么厉害的。人们常常将自己儿时的朋友一笔带过：“小学同学、初中一起玩的。。。
               但我觉得如果一个朋友你从小认识到现在关系都还不错，那说明你们真的不容易绝交。换句话来说，6/7年的交情可能不值一提，但从小开始的六七年的交情难得可贵。因为你们一起经历了人生变故最大的几年却仍然保持着联系。With that said, I think we are gonna be fine even when you go to new york or I'm on another planet. We already survived High School and College. What can be harder? Happy 21st birthday! And may our disconnected connection make the connection stronger.
            </p>
            <div class="firework"></div>
            <div class="firework"></div>
            <div class="firework"></div>
        {/if}
    </div>
</div>

<style>
    .container {
        position: fixed;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
    }

    .full-screen {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        margin: 0;
        overflow: hidden;
    }

    :global(.background-transition) {
        transition: background-color 0.5s ease;
    }

    :global(.bg-yellow) {
        background-color: rgb(240, 224, 0);
    }
    :global(.bg-green) {
        background-color: rgb(44, 202, 62);
    }

    @keyframes firework {
        0% {
            transform: translate(var(--x), var(--initialY));
            width: var(--initialSize);
            opacity: 1;
        }
        50% {
            width: 0.5vmin;
            opacity: 1;
        }
        100% {
            width: var(--finalSize);
            opacity: 0;
        }
    }

    .firework,
    .firework::before,
    .firework::after {
        --initialSize: 0.5vmin;
        --finalSize: 45vmin;
        --particleSize: 0.2vmin;
        --color1: yellow;
        --color2: khaki;
        --color3: white;
        --color4: lime;
        --color5: gold;
        --color6: mediumseagreen;
        --y: -30vmin;
        --x: -50%;
        --initialY: 60vmin;
        content: "";
        animation: firework 2s infinite;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, var(--y));
        width: var(--initialSize);
        aspect-ratio: 1;
        background: 
    /*
    radial-gradient(circle, var(--color1) var(--particleSize), #0000 0) 0% 0%,
    radial-gradient(circle, var(--color1) var(--particleSize), #0000 0) 100% 0%,
    radial-gradient(circle, var(--color1) var(--particleSize), #0000 0) 100% 100%,
    radial-gradient(circle, var(--color1) var(--particleSize), #0000 0) 0% 100%,
    */
            radial-gradient(circle, var(--color1) var(--particleSize), #0000 0)
                50% 0%,
            radial-gradient(circle, var(--color2) var(--particleSize), #0000 0)
                100% 50%,
            radial-gradient(circle, var(--color3) var(--particleSize), #0000 0)
                50% 100%,
            radial-gradient(circle, var(--color4) var(--particleSize), #0000 0)
                0% 50%,
            /* bottom right */
                radial-gradient(
                    circle,
                    var(--color5) var(--particleSize),
                    #0000 0
                )
                80% 90%,
            radial-gradient(circle, var(--color6) var(--particleSize), #0000 0)
                95% 90%,
            radial-gradient(circle, var(--color1) var(--particleSize), #0000 0)
                90% 70%,
            radial-gradient(circle, var(--color2) var(--particleSize), #0000 0)
                100% 60%,
            radial-gradient(circle, var(--color3) var(--particleSize), #0000 0)
                55% 80%,
            radial-gradient(circle, var(--color4) var(--particleSize), #0000 0)
                70% 77%,
            /* bottom left */
                radial-gradient(
                    circle,
                    var(--color5) var(--particleSize),
                    #0000 0
                )
                22% 90%,
            radial-gradient(circle, var(--color6) var(--particleSize), #0000 0)
                45% 90%,
            radial-gradient(circle, var(--color1) var(--particleSize), #0000 0)
                33% 70%,
            radial-gradient(circle, var(--color2) var(--particleSize), #0000 0)
                10% 60%,
            radial-gradient(circle, var(--color3) var(--particleSize), #0000 0)
                31% 80%,
            radial-gradient(circle, var(--color4) var(--particleSize), #0000 0)
                28% 77%,
            radial-gradient(circle, var(--color5) var(--particleSize), #0000 0)
                13% 72%,
            /* top left */
                radial-gradient(
                    circle,
                    var(--color6) var(--particleSize),
                    #0000 0
                )
                80% 10%,
            radial-gradient(circle, var(--color1) var(--particleSize), #0000 0)
                95% 14%,
            radial-gradient(circle, var(--color2) var(--particleSize), #0000 0)
                90% 23%,
            radial-gradient(circle, var(--color3) var(--particleSize), #0000 0)
                100% 43%,
            radial-gradient(circle, var(--color4) var(--particleSize), #0000 0)
                85% 27%,
            radial-gradient(circle, var(--color5) var(--particleSize), #0000 0)
                77% 37%,
            radial-gradient(circle, var(--color6) var(--particleSize), #0000 0)
                60% 7%,
            /* top right */
                radial-gradient(
                    circle,
                    var(--color1) var(--particleSize),
                    #0000 0
                )
                22% 14%,
            radial-gradient(circle, var(--color1) var(--particleSize), #0000 0)
                45% 20%,
            radial-gradient(circle, var(--color1) var(--particleSize), #0000 0)
                33% 34%,
            radial-gradient(circle, var(--color1) var(--particleSize), #0000 0)
                10% 29%,
            radial-gradient(circle, var(--color1) var(--particleSize), #0000 0)
                31% 37%,
            radial-gradient(circle, var(--color1) var(--particleSize), #0000 0)
                28% 7%,
            radial-gradient(circle, var(--color1) var(--particleSize), #0000 0)
                13% 42%;
        background-size: var(--initialSize) var(--initialSize);
        background-repeat: no-repeat;
    }

    .firework::before {
        --x: -50%;
        --y: -50%;
        --initialY: -50%;
        /*   transform: translate(-20vmin, -2vmin) rotate(40deg) scale(1.3) rotateY(40deg); */
        transform: translate(-50%, -50%) rotate(40deg) scale(1.3) rotateY(40deg);
        /*   animation: fireworkPseudo 2s infinite; */
    }

    .firework::after {
        --x: -50%;
        --y: -50%;
        --initialY: -50%;
        /*   transform: translate(44vmin, -50%) rotate(170deg) scale(1.15) rotateY(-30deg); */
        transform: translate(-50%, -50%) rotate(170deg) scale(1.15)
            rotateY(-30deg);
        /*   animation: fireworkPseudo 2s infinite; */
    }

    .firework:nth-child(2) {
        --x: 30vmin;
    }

    .firework:nth-child(2),
    .firework:nth-child(2)::before,
    .firework:nth-child(2)::after {
        --color1: pink;
        --color2: violet;
        --color3: fuchsia;
        --color4: orchid;
        --color5: plum;
        --color6: lavender;
        --finalSize: 40vmin;
        left: 30%;
        top: 60%;
        animation-delay: -0.25s;
    }

    .firework:nth-child(3) {
        --x: -30vmin;
        --y: -50vmin;
    }

    .firework:nth-child(3),
    .firework:nth-child(3)::before,
    .firework:nth-child(3)::after {
        --color1: cyan;
        --color2: lightcyan;
        --color3: lightblue;
        --color4: PaleTurquoise;
        --color5: SkyBlue;
        --color6: lavender;
        --finalSize: 35vmin;
        left: 70%;
        top: 60%;
        animation-delay: -0.4s;
    }
</style>
