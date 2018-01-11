<template lang="html">

    <transition-group tag="section" name="company" class="columns jokes-list" mode="out-in">

        <div class="column" v-for="(joke, index) in jokes" :key="joke.id">
            <div class="card">
                <div class="card-image">
                    <figure class="image">
                        <img :src="joke.images.original.gif_url" alt="Random images placeholder">
                    </figure>
                </div>
                <div class="card-content">
                    <div class="content">
                        <p class="tag is-primary">Rate: {{ joke.rating }}</p>
                        <h3>{{ joke.title }}</h3>
                    </div>
                </div>
                <div class="card-footer">
                    <a :href="joke.source" class="card-footer-item" target="_blank">Source</a>
                    <a :href="joke.user" class="card-footer-item">User</a>
                </div>
            </div>
        </div>

    </transition-group>

</template>

<script>

    export default {
        name: 'JokesList',
        props: ['jokes'],
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

    /* base */
    .company {
        backface-visibility: hidden;
        z-index: 1;
    }

    /* moving */
    .company-move {
        transition: all .3s ease-in-out 50ms;
    }

    /* appearing */
    .company-enter-active {
        transition: all .2s linear;
    }

    .company-enter-to {
        opacity: 1;
        transform: initial;
        transition: all .2s linear;
    }

    /* disappearing */
    .company-leave-active {
        transition: all .1s ease-in;
        position: absolute;
        z-index: 0;
    }

    /* appear at / disappear to */
    .company-enter,
    .company-leave-to {
        opacity: 0;
        transform: translateY(25px);
    }
</style>
