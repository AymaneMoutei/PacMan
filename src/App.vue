<script>
import grilleDef from "./constants/Grid.js";
import Fantome from "./components/Fantome.vue";
import Pacman from "./components/Pacman.vue";

import bleu from "./components/icons/fantome_bleu1.gif";
import rouge from "./components/icons/fantome_rouge1.gif";
import vert from "./components/icons/fantome_vert1.gif";
import orange from "./components/icons/fantome_orange1.gif";
import pacman from "./components/icons/pacman4.gif";
import { ref } from "vue";
const grille = ref(grilleDef);

import Grid from "./components/Grid.vue";

export default {
    components: {
        Grid,
        Fantome,
        Pacman,
    },
    data: () => ({
        grille,
        bleu,
        rouge,
        vert,
        orange,
        pacman,
    }),
    methods: {},
    setup() {
        function gameloop() {
            //this.$emit('move-fantome');
            window.dispatchEvent(new Event("move-fantome"));
            window.dispatchEvent(new Event("move-pacman"));
            setTimeout(gameloop, 120);
        }
        gameloop();
    },
};
</script>

<template>
    <main>
        <div
            style="
                position: fixed;
                top: 60%;
                left: 50%;
                transform: translate(-50%, -50%);
            "
        >
            <Grid :grille="grille">
                <Fantome :img="bleu" :grille="grille" />
                <Fantome :img="rouge" :grille="grille" />
                <Fantome :img="vert" :grille="grille" />
                <Fantome :img="orange" :grille="grille" />
                <Pacman :img="pacman" :grille="grille" />
            </Grid>
        </div>
    </main>
</template>

<style scoped></style>
