<template>
    <div>
        <!-- Page Header-->
        <header class="masthead" style="background-image: url('/img/home-bg.jpg')">
            <div class="container position-relative px-4 px-lg-5">
                <div class="row gx-4 gx-lg-5 justify-content-center">
                    <div class="col-md-10 col-lg-8 col-xl-7">
                        <div class="post-heading">
                            <h1>{{ title }}</h1>
                            <span class="meta">Publicado por {{ by }} el {{ date }}</span>
                        </div>
                    </div>
                </div>
            </div>
        </header>
        <div class="container px-4 px-lg-5">
            <div class="row gx-4 gx-lg-5 justify-content-center">
                <div class="col-md-10 col-lg-8 col-xl-7 text-justify">
                    <p v-for="(paragraph,key) in paragraphs" :key="`paragraph-${key}`">
                        <span v-html="paragraph.content"></span> <span v-if="paragraph.quote">({{paragraph.quote}})</span>
                    <ul v-if="paragraph.list">
                        <li v-for="(item,index) in paragraph.list" :key="`item-${key}-${index}`" v-html="item"></li>
                    </ul>
                    </p>
                    <!-- Divider-->
                    <hr class="my-4" />
                    <h2>Referecias</h2>
                    <p v-for="(reference,key) in references" :key="`reference-${key}`">
                        <a :href="reference.link">{{reference.title}}</a>
                    </p>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { usePostStore } from '@/stores/counter'
import posts from '@/data'

export default {
    data() {
        return {
            store: usePostStore(),
        }
    },
    props: {
        semana: {
            type: Number,
            default: 0,
        },
    },
    computed: {
        title: function () {
            return this.store.title
        },
        paragraphs: function () {
            return this.store.paragraphs
        },
        references: function () {
            return this.store.references
        },
        by: function () {
            return this.store.by
        },
        date: function () {
            return this.store.date
        },
    },
    mounted() {
        if (!this.store.title) {
            const post = posts[this.semana]
            this.store.title = post.title
            this.store.paragraphs = post.paragraphs
            this.store.references = post.references
            this.store.by = post.by
            this.store.date = post.date
        }
    }
}
</script>
<style scoped>
.text-justify {
    text-align: justify;
}
</style>