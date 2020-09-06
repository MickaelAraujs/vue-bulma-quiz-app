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
                            <p>some text related to the answers</p>

                            <ul class="list">
                                <li>Answer 1</li>
                                <li>Answer 2</li>
                                <li>Answer 3</li>
                                <li>Answer 4</li>
                                <li>Answer 5</li>
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
    export default {
        name: 'QuestionBox',

        props: {
            questionData: Object,
            next: Function,
        },
    }
</script>

<style scoped lang="scss">
    .header h6 {
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
</style>