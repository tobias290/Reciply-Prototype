<script>
    import { user } from "./stores/sessionStore";
    import { supabase } from "./business/supabaseClient";
    import { logOut } from "./business/auth";
    import LoggedOut from "./layouts/LoggedOut.svelte";
    import LoggedIn from "./layouts/LoggedIn.svelte";

    let showSignUp = false;

    user.set(supabase.auth.user());

    supabase.auth.onAuthStateChange((_, session) => {
        if (session)
            user.set(session.user);
        else
            user.set(null);
    });

    async function onLogOut() {
        const { error } = logOut();

        if (error)
            console.log(error)
    }
</script>

<header class="header" class:header--small={$user}>
    <h1 class="header__title">Reciply</h1>
    {#if $user}
        <i class="fas fa-sign-out-alt logout" on:click={onLogOut}></i>
    {/if}
</header>
<main>
    {#if $user}
        <LoggedIn />
    {:else}
        <LoggedOut />
    {/if}
</main>


<style lang="scss">
	@import "css/bootstrap";

	*:not(i) {
		font-family: $font-primary;
	}

    :global(body) {
        @include flex($direction: column);

        background: $color-primary;
        overflow: hidden;
    }

    .header {
        @include flex($center: true);

        box-sizing: border-box;
        height: 175px;
        padding: 0 1rem 30px 1rem;
        transition: height .25s linear;

        &__title {
            color: $color-white;
            font-size: 4.5rem;
            font-family: $font-title !important;
            transition: font-size .25s linear;
        }

        &--small {
            @include flex($align: center, $justify: space-between);

            height: 90px;

            .header__title {
                font-size: 1.5rem;
            }
        }

        .logout {
            color: $color-white;
            font-size: 1.5rem;
        }
    }

    main {
        background: $color-white;
        border-radius: 16px 16px 0 0;
        box-sizing: border-box;
        flex-grow: 1;
        margin-top: -30px;
        padding: 1rem;
        overflow: auto;
    }
</style>
