<script>
import { getRandomIntInclusive } from "../constants/Grid.js";
import { ref } from "vue";
// const x = ref(9);
// const y = ref(11);
// const direction = ref(0);

export default {
    props: {
        img: String,
        grille: Array,
    },
    data() {
        return {
            img: this.img,
            x: 9,
            y: 11,
            direction: 0,
            //grille : this.grille,
        };
    },
    computed: {},
    methods: {
        collisionFantome() {
            //fixed out of range error (1 indexed ?)
            if (this.direction == 0) {
                if (
                    this.x > this.grille[0].length ||
                    this.grille[this.y - 1][this.x - 1] == 0
                )
                    this.x--;
            } else if (this.direction == 1) {
                if (this.x < 1 || this.grille[this.y - 1][this.x - 1] == 0)
                    this.x++;
            } else if (this.direction == 2) {
                if (
                    this.y > this.grille.length ||
                    this.grille[this.y - 1][this.x - 1] == 0
                )
                    this.y--;
            } else if (this.direction == 3)
                if (this.y < 1 || this.grille[this.y - 1][this.x - 1] == 0)
                    this.y++;
        },
        bougeFantome() {
            this.direction = getRandomIntInclusive(0, 3);
            if (this.direction == 0) this.x++;
            else if (this.direction == 1) this.x--;
            else if (this.direction == 2) this.y++;
            else if (this.direction == 3) this.y--;
            this.collisionFantome();
            // console.log({x:this.x,y:this.y});
            //this.$forceUpdate();
        },
        handleTouch(event) {
            //console.log(event);
            if (event.detail.x == this.x && event.detail.y == this.y)
                alert("YOU LOST !!");
        },
    },
    mounted: function mounted() {
        window.addEventListener("move-pacman", this.bougeFantome);
        window.addEventListener("ghost-pacman", this.handleTouch);
    },
};
</script>

<template>
    <img :src="img" :style="{ gridColumn: x, gridRow: y }" />
</template>

<style></style>
