<template>
    <header class="header">
        <nav class="navbar is-info" role="navigation" aria-label="main navigation"> 
            <div class="navbar-menu">
                <div class="navbar-start">
                    <a class="navbar-item brand">
                        Awesome Random Quiz
                    </a>

                    <a class="navbar-item is-tab is-active">
                        Counter: {{correctAnswers}}/{{totalQuestions}}
                    </a>
                </div>
            </div>
        </nav>
    </header>
</template>

<script>
    export default {
        name: 'Header',

        props: [
            'correctAnswers',
            'totalQuestions'
        ]
    }
</script>

<style scoped lang="scss">
</style>