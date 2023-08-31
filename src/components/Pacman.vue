<script>
import { getRandomIntInclusive } from "../constants/Grid.js";
import { ref } from "vue";

export default {
    props: {
        img: String,
        grille: Array,
    },
    data() {
        return {
            img: this.img,
            x: 5,
            y: 2,
            direction: 0,
            score: 0,
            nombreBombon: 178,
            //this.grille : this.this.grille,
        };
    },
    computed: {},
    methods: {
        appuieTouche(event) {
            //console.log(event.key);
            switch (event.key) {
                case "d":
                case "D":
                    this.direction = 0;
                    break;
                case "q":
                case "D":
                    this.direction = 1;
                    break;
                case "z":
                case "Z":
                    this.direction = 3;
                    break;
                case "s":
                case "S":
                    this.direction = 2;
                    break;
            }
        },
        sortMur() {
            if (this.x > this.grille[0].length) this.x = 1;
            if (this.x < 1) this.x = this.grille[0].length;
        },

        mangeBonbon() {
            if (this.grille[this.y - 1][this.x - 1] == 2) {
                this.grille[this.y - 1][this.x - 1] = 1;
                this.nombreBombon--;
                this.score++;
            }
        },
        collisionPacMan() {
            //console.log({x:this.x,y:this.y});
            if (this.direction == 0) {
                if (this.grille[this.y - 1][this.x - 1] == 0) this.x--;
            } else if (this.direction == 1) {
                if (this.grille[this.y - 1][this.x - 1] == 0) this.x++;
            } else if (this.direction == 2) {
                if (this.grille[this.y - 1][this.x - 1] == 0) this.y--;
            } else if (this.direction == 3)
                if (this.grille[this.y - 1][this.x - 1] == 0) this.y++;
        },
        bougePacMan() {
            if (this.nombreBombon == 0) {
                alert("YOU WOOOOOON !!");
            }
            console.log(this.nombreBombon);
            if (this.direction == 0) this.x++;
            else if (this.direction == 1) this.x--;
            else if (this.direction == 2) this.y++;
            else if (this.direction == 3) this.y--;
            this.collisionPacMan();
            this.sortMur();
            this.mangeBonbon();
            window.dispatchEvent(
                new CustomEvent("ghost-pacman", {
                    detail: { x: this.x, y: this.y },
                })
            );
        },
    },
    mounted: function mounted() {
        window.addEventListener("keydown", this.appuieTouche);
        window.addEventListener("move-pacman", this.bougePacMan);
    },
};
</script>

<template>
    <div style="height: 400px; width: 400px">
        <p class="score">Votre score est: {{ this.score }}</p>
    </div>
    <img :src="img" :style="{ gridColumn: x, gridRow: y }" />
</template>

<style>
.score {
    color: #4c4a37;
    font-family: "Source Sans Pro", sans-serif;
    font-size: 30px;
    line-height: 32px;
    margin: 0 0 24px;
    text-align: center;
}
</style>
