<template>
    <div id="app">
        <!-- <header>
            <span>Masuk ke Dalam</span>
        </header> -->
        <main>


            <section class="hero is-success is-fullheight">
                <div class="hero-body">
                    <div class="container">


                        <div class="page-title">
                            <img src="./assets/sun.png" alt="Logo" width="50">
                            <h2 class="title">GIF Buat Kamu</h2>
                            <h4 class="subtitle">disajikan tiap hari &mdash; kapanpun kamu mau</h4>
                        </div>

                        <div class="columns is-centered">

                            <div class="column is-two-thirds">

                                <div class="level page-intro">
                                    <div class="level-item">
                                        <div>
                                            <label>Lihat GIF yang Lagi Trending</label>
                                            <button id="btn" class="button is-primary" @click="getJokes">Lihat</button>
                                        </div>
                                    </div>
                                    <div class="level-item">
                                        atau...
                                    </div>
                                    <div class="level-item">
                                        <form class="form" @submit.prevent="onSubmit">
                                            <div class="field has-addons">
                                                <div class="control">
                                                    <input class="input" v-model="newSearch" type="text" placeholder="Cari apa aja deh...">
                                                </div>
                                                <div class="control">
                                                    <input type="submit" value="Cari" class="button is-primary">
                                                </div>
                                            </div>
                                            <div class="help is-danger" v-if="searchErrorMessage">
                                                Isi dulu kelesss
                                            </div>
                                            <div class="search-resolved" v-if="searchResolved">
                                                Eh ada ketemu {{ jokes.length }} GIF nih buat kata kunci {{ lastSearch }}.
                                            </div>
                                        </form>
                                    </div>

                                </div>

                            </div> <!-- kelar Column is-Half -->

                        </div>


                        <div v-if="loading" class="loading-state">
                            <img src="../src/assets/loader.gif"/>
                        </div>

                        <jokes-list :jokes="jokes"></jokes-list>

                    </div>
                </div>
            </section>

        </main>
    </div>
</template>

<script>
    import axios from 'axios';
    import JokesList from './JokesList.vue';

    const GphApiClient = require('giphy-js-sdk-core');
    const client = GphApiClient("OXqpSPdihtQBjAjBIzWWEavgT2W0fJ62");

    export default {
        name: 'app',
        components: {
            'jokes-list': JokesList
        },
        data () {
            return {
                jokes: [],
                loading: false,
                newSearch: '',
                lastSearch: '',
                searchLimit: 100,
                searchResolved: false,
                searchErrorMessage: false
            }
        },
        methods: {
            getJokes: function() {
                this.loading = true;
                client.trending('gifs', {}).then(response =>  {
                    this.loading = false;
                    this.jokes = response.data;
                    console.log(response);
                }).catch(error =>  {
                    console.log(error);
                    this.loading = false;
                })
            },
            onSubmit: function() {
                if (this.newSearch.length) {
                    this.loading = true
                    client.search('gifs', {"q": this.newSearch, "limit": this.searchLimit}).then(response => {
                        this.loading = false
                        this.searchResolved = true
                        this.lastSearch = this.newSearch
                        this.jokes = response.data
                        this.searchErrorMessage = false
                    })
                } else {
                    this.searchErrorMessage = true
                }
            }
        }
        // mounted: function() {
        //     this.getJokes();
        // }
    }
</script>

<style lang="scss">
    body {
        margin: 0;
        background-color: #23d160 !important;
    }

    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        color: #2c3e50;
    }

    main {
        text-align: center;
    }

    .page-title {
        margin-bottom: 4em;
        .title {
            font-size: 3rem;
            color: #7957d5 !important;
        }
        img {
            animation: rotator 3s infinite linear;
        }
    }

    header {
        margin: 0;
        height: 56px;
        padding: 0 16px 0 24px;
        background-color: #35495E;
        color: #ffffff;
        span {
            display: block;
            position: relative;
            font-size: 20px;
            line-height: 1;
            letter-spacing: .02em;
            font-weight: 400;
            box-sizing: border-box;
            padding-top: 16px;
        }
    }

    .hero {
        .form {
            // margin-bottom: 3em;
        }
    }

    .loading-state {
        margin-bottom: 3em;
    }

    button {
        background: #51B767;
        color: #ffffff;
        padding: 15px;
        border-radius: 0;
        font-weight: bold;
        font-size: 15px;
        border: 0;
    }

    .cards {
        background: #F5F5F5;
        height:400px;
        &:hover {
            transform: translateY(-0.5em);
            background: #EBEBEB;
        }
    }

    .cards {
        column-count: 1;
        column-gap: 1em;
        margin-top: 70px;
    }

    // .columns {
    //     .column {
    //         flex-basis: 23%;
    //     }
    // }

    .page-intro {
        margin-bottom: 3em;
        .level-item {
            > div {
                display: flex;
                flex-direction: column;
            }
            label {
                margin-bottom: .5em;
            }
        }
    }

    @keyframes rotator {
        from {
            transform: rotate(0);
        }
        to {
            transform: rotate(360deg);
        }
    }
</style>
