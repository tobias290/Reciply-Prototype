<script>
    import { createEventDispatcher } from "svelte";

    export let active;
    export let addRecipe;

    const dispatch = createEventDispatcher();

    function tab(name) {
        dispatch("tabClick", name)
    }
</script>

<nav class="tabs">
    <ul class="tabs__items">
        <li
            class="tabs__item"
            class:tabs__item--active={active === "home"}
            on:click={() => tab("home")}
        ><i class="fas fa-home"></i></li>
        <li
            class="tabs__item"
            class:tabs__item--active={active === "shopping-list"}
            on:click={() => tab("shopping-list")}>
            <i class="fas fa-list-alt"></i></li>
        <li
            class="tabs__item"
            class:tabs__item--active={active === "weekly-planner"}
            on:click={() => tab("weekly-planner")}
        ><i class="fas fa-calendar-week"></i></li>
        <li
            class="tabs__item"
            class:tabs__item--active={active === "settings"}
            on:click={() => tab("settings")}
        ><i class="fas fa-cog"></i></li>
        <li
            class="tabs__item tabs__new tabs__new--active"
            class:tabs__new--active={addRecipe}
            on:click={() => dispatch("addRecipe")}
        ><i class="fas fa-plus"></i></li>
    </ul>
</nav>

<style lang="scss">
    @import "../css/bootstrap";

    .tabs {
        @include center;

        background: $color-white;
        border-radius: 30px;
        bottom: 10px;
        box-shadow: 0 0 16px 0 rgba(black, .25);
        height: 60px;
        max-width: 350px;
        position: fixed;
        width: 100%;
        z-index: 1000;

        &__items {
            @include flex($align: center, $justify: space-between);

            list-style: none;
            margin: 0;
            padding-left: 30px;
        }

        &__item {
            color: #BBB;
            cursor: pointer;
            font-size: 1.25rem;
            transition: color .125s ease-in-out, transform .125s ease-in-out;

            &--active {
                color: $color-grey;
                transform: scale(1.25);
            }
        }

        &__new {
            @include flex($center: true);

            background: $color-primary;
            border-radius: 30px;
            color: $color-white;
            height: 60px;
            margin-left: -20px;
            transition: background .125s linear;
            width: 60px;

            & > i {
                transition: transform .125s linear;
            }

            &--active  {
                background: $color-red;

                i {
                    transform: rotate(45deg);
                }
            }
        }
    }
</style>
