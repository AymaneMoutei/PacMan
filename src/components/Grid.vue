<script>
export default {
    props: {
        grille: Array,
    },
    data(instance) {
        //console.log(instance.grille);
        return {
            grille: instance.grille,
            dum_column: `repeat(${instance.grille[0].length}, 40px)`,
            dum_row: `repeat(${instance.grille.length}, 40px)`,
        };
    },
    computed: {},
    methods: {},
};
</script>

<template :key="grille">
    <div class="grid">
        <template v-for="(row, j) in grille" :key="row">
            <template v-for="(cur, i) in row" :key="cur">
                <div
                    :class="{
                        mur: cur === 0,
                        sol: cur == 1,
                        bonbon: cur == 2,
                    }"
                    :style="{
                        gridColumn: i + 1,
                        gridRow: j + 1,
                    }"
                ></div>
            </template>
        </template>
        <slot />
    </div>
</template>

<style>
.grid {
    grid-template-columns: v-bind(dum_column);
    grid-template-rows: v-bind(dum_row);
    display: grid;
    margin-left: 150px;
    margin-top: 5%;
}
.mur {
    background-image: url(./icons/murbrique.jpg);
}
.sol {
    background-color: black;
}
.bonbon {
    background-image: url(./icons/bonbon.gif);
}
</style>
