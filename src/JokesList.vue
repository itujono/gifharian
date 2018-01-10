<template lang="html">
    <section class="columns jokes-list">

        <div class="column" v-for="(joke, index) in jokes" :key="joke.id" @click="deleteJokes(index)">
            <div class="card">
                <div class="card-image">
                    <figure class="image">
                        <img :src="joke.images.original.gif_url" alt="Random images placeholder">
                    </figure>
                </div>
                <div class="card-content">
                    <div class="content">
                        <p>{{ joke.rating }}</p>
                        <h3>{{ joke.title }}</h3>
                        <p><a :href="joke.source">Source</a></p>
                        <!-- <p>{{ joke.user["username"] }}</p> -->
                    </div>
                </div>
            </div>
        </div>

    </section>
</template>

<script>
    export default {
        name: 'JokesList',
        props: ['jokes'],
        // filters: {
        //     upperCasing(value) {
        //         return value.charAt(0).toUpperCase() + value.slice(1)
        //     }
        // },
        methods: {
            // deleteJokes: function(index) {
            //     this.jokes.splice(index, 1)
            //     console.log(index)
            // }
        }
    }
</script>

<style lang="scss">
    .jokes-list.columns {
        flex-wrap: wrap;
        justify-content: center;
        .column {
            flex-basis: 23%;
            flex-grow: 0;
            .card {
                height: 100%;
            }
        }
        .image {
            max-height: 200px;
            overflow: hidden;
            img {
                object-fit: cover;
                min-height: 200px;
            }
        }
        .content {
            h3 {
                margin-top: 5px;
            }
        }
    }
</style>
