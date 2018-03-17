<template>
    <div class="w-full h-screen justify-center items-center p-8 " :class="backgroundClass">
        <div class="w-full text-5xl text-grey-lightest flex justify-center">
            Number Flash
        </div>

        <div v-if="!playing">
            <div class="flex justify-center flex-col md:flex-row">
                <div class="text-4xl text-center text-grey-lightest px-4 py-2 m-2 max-w-full">
                    <label class="block pb-2">Start</label>

                    <input type="number" v-model="start" class="appearance-none p-8 text-center max-w-full">
                </div>

                <div class="text-4xl text-center text-grey-lightest px-4 py-2 m-2 max-w-full">
                    <label class="block pb-2">End</label>

                    <input type="number" v-model="end" class="appearance-none p-8 text-center max-w-full">
                </div>
            </div>


            <div class="flex justify-center mt-8">
                <div class="w-full text-4xl text-grey-lightest flex justify-center">
                    <input type="checkbox"
                           class="mr-2 mt-4"
                           v-model="random"
                    />
                    Random Order
                </div>
            </div>

            <div class="flex justify-center mt-8">
                <div class="w-1/2 text-4xl text-grey-lightest flex justify-center">
                    <button class="px-4 py-2 bg-green rounded text-grey-lightest shadow-md" @click="playGame">
                        Play
                    </button>
                </div>
            </div>
        </div>

        <div v-else class="text-12xl text-center text-grey-lightest mt-8">
            <span class="block">
                {{ currentNumber }}
            </span>

            <button class="px-4 py-2 bg-green rounded text-grey-lightest shadow-md text-4xl" @click="nextNumber">
                Next
            </button>

            <button class="px-4 py-2 bg-red rounded text-grey-lightest shadow-md text-4xl" @click="reset">
                Reset
            </button>
        </div>
    </div>
</template>

<script>
    export default {
        computed: {
            backgroundClass() {
                let object = {}

                object[this.background] = true

                return object
            },
        },
        data() {
            return {
                currentNumber: 0,
                random: false,
                playing: false,
                background: 'bg-red-light',
                start: 0,
                end: 20,
                colors: [
                    'red',
                    'orange',
                    'green',
                    'teal',
                    'blue',
                    'indigo',
                    'purple',
                    'pink',
                ],
            }
        },
        methods: {
            reset() {
                this.currentNumber = 0
                this.random = false
                this.playing = false
                this.start = 0
                this.end = 20
            },

            nextNumber() {
                this.setBackgroundColor()

                if (this.random) {
                    this.currentNumber = Math.floor(Math.random() * (parseInt(this.end) - parseInt(this.start) + 1) + parseInt(this.start))
                } else {
                    if (this.currentNumber === this.end) {
                        return this.reset()
                    }

                    this.currentNumber++
                }
            },
            playGame() {
                this.playing = true

                this.setBackgroundColor()

                this.currentNumber = this.start
            },
            setBackgroundColor() {
                this.background = 'bg-' + this.colors[Math.floor((Math.random() * 7))] + '-light'
            },
        },
        mounted() {
            this.setBackgroundColor()
        },
    }
</script>
