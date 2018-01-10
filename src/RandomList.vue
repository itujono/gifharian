<template lang="html">
    <section class="columns jokes-list" id="randoms">

        <div class="column" :key="randoms.id">
            <div class="card">
                <div class="card-image">
                    <figure class="image">
                        <!-- <img :src="randoms.images.original.gif_url" alt="Random images placeholder"> -->
                    </figure>
                </div>
                <div class="card-content">
                    <div class="content">
                        <p class="tag is-primary">Rate: {{ randoms.rating }}</p>
                        <h3>{{ randoms.title }}</h3>
                    </div>
                </div>
                <div class="card-footer">
                    <a :href="randoms.source" class="card-footer-item">Source</a>
                    <a :href="randoms.user" class="card-footer-item">User</a>
                </div>
            </div>
        </div>

    </section>
</template>

<script>
    export default {
        name: 'RandomList',
        props: ['randoms'],
        // data() {
        //     return {
        //         trendingResolved: false,
        //         randomResolved: false
        //     }
        // },
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
        .card-content {
            padding: .5rem;
        }
        .content {
            h3 {
                font-size: 1em;
                margin-top: 5px;
            }
        }
    }
</style>
