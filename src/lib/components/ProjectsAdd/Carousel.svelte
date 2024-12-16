<script lang="ts">
    import { onMount, tick } from "svelte";

    export let initialItems: string[] = ["Start"];
    export let title: string = "title";
    let items = initialItems;
    let initialTitle = title;

    let carousel: HTMLElement;
    let currentIndex = 0;

    function addItem(): void {
        const newItem = generateRandomString();
        items = [...items, newItem];
        scrollToIndex(0);
    }

    function generateRandomString(length: number = 5): string {
        const characters =
            "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789";
        return Array(length)
            .fill(null)
            .map(
                () => characters[Math.floor(Math.random() * characters.length)],
            )
            .join("");
    }

    function scrollToIndex(index: number): void {
        if (!carousel) return;

        const itemWidth = 400 + 10;
        const scrollPosition = index * itemWidth;

        carousel.scrollTo({
            left: scrollPosition,
            behavior: "smooth",
        });

        currentIndex = index;
    }

    function handleWheel(event: WheelEvent): void {
        event.preventDefault();

        if (event.deltaY > 0) {
            if (currentIndex < items.length - 1) {
                scrollToIndex(currentIndex + 1);
            }
        } else {
            if (currentIndex > 0) {
                scrollToIndex(currentIndex - 1);
            }
        }
    }

    function handleKeydown(event: KeyboardEvent): void {
        if (event.key === "ArrowRight") {
            if (currentIndex < items.length - 1) {
                scrollToIndex(currentIndex + 1);
            }
        } else if (event.key === "ArrowLeft") {
            if (currentIndex > 0) {
                scrollToIndex(currentIndex - 1);
            }
        }
    }

    onMount(() => {
        window.addEventListener("keydown", handleKeydown);

        if (carousel) {
            carousel.addEventListener("wheel", handleWheel, { passive: false });
        }

        return () => {
            window.removeEventListener("keydown", handleKeydown);
            if (carousel) {
                carousel.removeEventListener("wheel", handleWheel);
            }
        };
    });
</script>

<div class="main-container">
    <div class="carousel-header">
        <div class="header-content">
            <div class="title">
                <h1>{initialTitle}</h1>
            </div>
            <input type="text" class="search-bar" placeholder="Search" />
        </div>
    </div>

    <div class="carousel-container" bind:this={carousel}>
        <div class="carousel-item add-item" on:click={addItem}>Add Item</div>

        {#each items as item, index (item)}
            <div class="carousel-item" class:active={index === currentIndex}>
                {item}
            </div>
        {/each}
    </div>
</div>

<style>
    .carousel-header {
        display: flex;
        justify-content: center;
        align-items: center;
        padding: 10px 4px;
        width: 100%;
    }

    .header-content {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        gap: 10px;
        margin-right: auto;
    }

    .title h1 {
        margin: 0;
        text-align: left;
        font-size: 24px;
    }

    .search-bar {
        width: 300px;
        padding: 5px;
        font-size: 16px;
        text-align: left;
    }

    .carousel-container {
        display: flex;
        width: 100vw;
        overflow: hidden;
        gap: 10px;
        scroll-snap-type: x mandatory;
        padding: 20px 4px;
        scroll-behavior: smooth;
    }

    .carousel-item {
        flex: 0 0 400px;
        height: 150px;
        background-color: #4caf50;
        color: white;
        display: flex;
        justify-content: center;
        align-items: center;
        text-transform: uppercase;
        font-weight: bold;
        border-radius: 8px;
        scroll-snap-align: center;
        transition: all 0.3s ease;
    }

    .carousel-item.active {
        transform: scale(1);
        box-shadow: 0 0 15px rgba(0, 0, 0, 0.3);
    }

    .add-item {
        background-color: #007bff;
        cursor: pointer;
    }

    .carousel-item:hover {
        transform: scale(1.02);
    }

    .main-container {
        width: 95vw;
    }
</style>
