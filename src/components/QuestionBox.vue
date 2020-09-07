<template>
    <div class="box">
        <article class="media">
            <div class="media-content">
                <div class="content">
                    <section class="section">
                        <header class="header">
                            <h6>
                                {{questionData.question}}
                            </h6>
                        </header>

                        <main class="main">
                            <p>Click on the answer you think it's the right one.</p>

                            <ul class="list">
                                <li v-for="(answer, index) in answers" :key="index">
                                    <button
                                        class="button"
                                        @click="handleSelectedIndex(index)"
                                        :class="[selectedIndex === index && 'selected']"
                                    >
                                        {{answer}}
                                    </button>
                                </li>
                            </ul>
                        </main>

                        <div class="columns">
                            <button class="button column is-3 is-info">
                                submit
                            </button>

                            <button
                                class="button column is-3 is-success"
                                v-on:click="next"
                            >
                                next
                            </button>
                        </div>
                    </section>
                </div>
            </div>
        </article>
    </div>
</template>

<script>
    import _ from 'lodash'
    export default {
        name: 'QuestionBox',

        props: {
            questionData: Object,
            next: Function,
        },

        data() {
            return {
                selectedIndex: null,
                shuffledAnswers: [],
            }
        },

        methods: {
            handleSelectedIndex(index) {
                this.selectedIndex = index;
            },

            shuffleAnswers() {
                const answers = [...this.questionData.incorrect_answers, this.questionData.correct_answer];
                
                this.shuffledAnswers = _.shuffle(answers);
            }
        },

        computed: {
            answers() {
                const answers = [...this.questionData.incorrect_answers, this.questionData.correct_answer];

                return answers;
            }
        },

        watch: {
            questionData: {
                immediate: true,
                handler() {
                    this.selectedIndex = null;
                    this.shuffleAnswers();
                }
            }
        },
    }
</script>

<style scoped lang="scss">
    .header h6, .main p {
        text-align: center;
    }

    .columns {
        margin-top: 1.4rem;
        padding: 1rem 1.6rem;    
        justify-content: center;
    }

    .box {
        margin: 4rem;
    }

    .button {
        display: flex;
        font-weight: bold;
    }

    .button + .button {
        margin-left: 4rem;
    }

    .list {
        list-style: none;
    }

    .list * {
        width: 100%;
        margin-top: 1.2rem;
    }

    .correct {
        background-color: #77BD8B;
    }

    .incorrect {
        background-color: #BC0022;
    }

    .selected {
        background-color: #5199FF;
    }
</style>