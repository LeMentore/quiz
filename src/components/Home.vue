<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-md-6">
                <h1 class="text-center">The super quiz</h1>
            </div>
        </div>
        <hr>
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-md-6">
                <transition name="flip" mode="out-in">
                    <component :is="mode" @answered="answered($event)" @confirmed="mode = 'app-question'"></component>
                </transition>
            </div>
        </div>
    </div>
</template>

<script>
    import Question from './Question'
    import Answer from './Answer'

    export default {
        data() {
            return {
                mode: 'app-question'
            }
        },
        methods: {
            answered(isCorrect){
                if(isCorrect){
                    this.mode = 'app-answer'
                } else {
                    this.mode = 'app-question'
                    alert('Wrong, try again!')
                }
            }
        },
        components: {
            appQuestion: Question,
            appAnswer: Answer
        }
    }
</script>

<style>
    .flip-enter {

    }
    .flip-enter-active {
        animation: flip-in 0.2s ease-out forwards;
    }
    .flip-leave {

    }
    .flip-leave-active {
        animation: flip-out 0.2s ease-out forwards;
    }

    @keyframes flip-out {
        from {
            transform: rotateY(0deg);
        }
        to {
            transform: rotateY(90deg);
        }
    }

    @keyframes flip-in {
        from {
            transform: rotateY(90deg);
        }
        to {
            transform: rotateY(0deg);
        }
    }
</style>
