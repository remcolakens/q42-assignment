<template>
    <div>
        <img src="../assets/background.jpg" class="background" alt="background" />

        <div class="logo-wrapper">
            <img src="../assets/logo.png" class="logo" alt="logo" />
        </div>

        <div class="grid">
            <div class="row" v-for="(row, rowKey) in grid">
                <div
                    class="cell"
                    v-for="(cell, cellKey) in row"
                    :class="checkFibonacci(cell, rowKey, cellKey)"
                    @click="gridIncrement(rowKey, cellKey, $event)">
                    {{ cell }}
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { TweenLite } from "gsap";

export default {
    name: "Fibonacci",

    data() {
        return {
            grid: {
                // You can adjust the grid and values here, they are also reactive which is awesome!
                1:  { 1: null, 2: null, 3: null, 4: null, 5: null, 6: null, 7: null, 8: null, 9: null },
                2:  { 1: null, 2: null, 3: null, 4: null, 5: null, 6: null, 7: null, 8: null, 9: null },
                3:  { 1: null, 2: null, 3: null, 4: null, 5: null, 6: null, 7: null, 8: null, 9: null },
                4:  { 1: null, 2: null, 3: null, 4: null, 5: null, 6: null, 7: null, 8: null, 9: null },
                5:  { 1: null, 2: null, 3: null, 4: null, 5: null, 6: null, 7: null, 8: null, 9: null },
                6:  { 1: null, 2: null, 3: null, 4: null, 5: null, 6: null, 7: null, 8: null, 9: null },
                7:  { 1: null, 2: null, 3: null, 4: null, 5: null, 6: null, 7: null, 8: null, 9: null },
                8:  { 1: null, 2: null, 3: null, 4: null, 5: null, 6: null, 7: null, 8: null, 9: null },
                9:  { 1: null, 2: null, 3: null, 4: null, 5: null, 6: null, 7: null, 8: null, 9: null },
            }
        };
    },

    methods: {
        // Method for calculating Fibonacci numbers
        checkFibonacci(cell, rowKey, cellKey) {
            // These are all the values we need for our calculations
            let cell1 = this.grid[rowKey][cellKey];
            let cell2 = this.grid[rowKey][cellKey - 1];
            let cell3 = this.grid[rowKey][cellKey - 2];
            let cell4 = this.grid[rowKey][cellKey - 3];
            let cell5 = this.grid[rowKey][cellKey - 4];

            // We dont want to check empty values right?
            if(cell1 && cell2 && cell3 && cell4 && cell5) {
                // THIRD cell equal to 1 + 2
                let fibonacciSequence1 = cell3 === cell1 + cell2;

                // FIFTH cell equal to 4 + 5
                let fibonacciSequence2 = cell5 === cell3 + cell4;

                // Do we have a match?
                if(fibonacciSequence1 && fibonacciSequence2) {
                    // Fibonacci-sequence in 5
                    for (let i = 1; i <= 5; i++) {
                        // Target DOM element
                        let element = document.querySelector(`.row:nth-child(${rowKey}) .cell:nth-child(${cellKey}`);

                        // Animate color
                        this.addColor(element, "#03a810");

                        // Reset the value to null
                        this.grid[rowKey][cellKey] = null;

                        // Lets go backwards
                        cellKey--;
                    }
                }
            }
        },

        // JS color change ^^
        addColor(target, color) {
            // Tween value
            TweenLite.to(target, 0.4, {
                css: { backgroundColor: color }
            });

            // Default value
            TweenLite.to(target, 0.4, {
                css: { backgroundColor: "rgba(236, 236, 236, 0.9)" },
                delay: 0.4
            });
        },

        // Increase X & Y-axis by 1
        gridIncrement(rowKey, cellKey, event) {
            // On click we trigger color tween
            this.addColor(event.target, "#ffc729");

            // We need to correct the number otherwise it would be always +2
            this.grid[rowKey][cellKey]--;

            // Loop through X-axis (ES6)
            Object.keys(this.grid[rowKey]).map(i => {
                this.grid[rowKey][i]++;
            });

            // Loop through Y-axis (ES6)
            Object.keys(this.grid).map(i => {
                this.grid[i][cellKey]++;
            });
        }
    }
};
</script>

<style scoped lang="scss">
@import url('https://fonts.googleapis.com/css?family=Press+Start+2P');

$total-grid-cells: 10;
$cell-height: 50px;
$color-grey: #ececec;
$color-yellow: #ffc729;

.logo-wrapper {
    display: flex;
    justify-content: center;
    width: 100%;
    position: fixed;
    top: 50px;
}

.background {
    width: 100vw;
    height: 100vh;
    object-fit: cover;
    object-position: bottom center;
}

.grid {
    width: calc(#{$cell-height} * #{$total-grid-cells});
    top: 50%;
    right: 50%;
    position: absolute;
    transform: translate(50%, -50%);
    border: 10px solid $color-yellow;
}

.row {
    display: flex;
}

.cell {
    background: rgba($color-grey, 0.9);
    flex: 1;
    cursor: pointer;
    font-family: 'Press Start 2P', cursive;
    font-size: 1.4rem;
    font-weight: 800;
    height: $cell-height;
    display: flex;
    align-items: center;
    justify-content: center;

    &:hover {
        background: darken($color-grey, 15%);
    }
}
</style>
