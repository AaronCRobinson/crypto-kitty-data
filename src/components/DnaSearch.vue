<template>
    <div class="container">
        <h1 class="title">DNA Search</h1>
        <div class="columns">
            <div class="column">
                <div class="field">
                    <label class="label">Cattribute</label>
                    <div class="control">
                        <input class="input" id="cattribute" type="text" v-model="cattribute" v-on:click="setupAutoComplete">
                    </div>
                </div>
                <div class="field">
                    <label class="checkbox">
                        <input type="checkbox" v-model="d0">
                        D0
                    </label>
                    <label class="checkbox">
                        <input type="checkbox" v-model="r1">
                        R1
                    </label>
                    <label class="checkbox">
                        <input type="checkbox" v-model="r2">
                        R2
                    </label>
                    <label class="checkbox">
                        <input type="checkbox" v-model="r3">
                        R3
                    </label>
                    <div class="is-pulled-right">
                        <a class="button is-link" v-on:click="addParam">Add</a>
                    </div>
                </div>

            </div>
            <div class="column is-2">
                <div class="field">
                    <label class="label">Generation</label>
                    <div class="control">
                        <input class="input" type="text" v-model="gen">
                    </div>
                </div>
                <div class="field is-grouped">
                    <div class="control">
                        <a class="button is-link" v-on:click="addGen(gen)">Add Generation</a>
                    </div>
                </div>
            </div>
            <div class="column is-2">
                <div class="field">
                    <label class="label">Page</label>
                    <div class="control">
                        <input class="input" type="text" v-model="offset">
                    </div>
                </div>
                <div class="field">
                    <label class="label">
                        Count: {{ count }} / 100
                    </label>
                </div>
            </div>
            <div class="column">
                <div class="field">
                    <label class="label">Query</label>
                    <div class="control">
                        <input class="input" type="text" v-model="queryString">
                    </div>
                </div>

                <div class="field is-grouped">
                    <div class="control">
                        <a class="button is-link" v-on:click="search" v-bind:class="{ 'is-loading' : isSearching  }">Search</a>
                    </div>
                </div>
            </div>

        </div>
        <!-- Main container -->
        <table class="table is-bordered is-striped is-narrow is-hoverable ">
            <thead>
            <tr>
                <th colspan="3"></th>

                <th colspan="4" class="cattribute-border-left">Fur</th>

                <th colspan="4" class="cattribute-border-left">Pattern</th>

                <th colspan="4" class="cattribute-border-left">Eye-Color</th>

                <th colspan="4" class="cattribute-border-left">Eye-Type</th>

                <th colspan="4" class="cattribute-border-left">Base-Color</th>

                <th colspan="4" class="cattribute-border-left">HighLi-Col</th>

                <th colspan="4" class="cattribute-border-left">Accent-Col</th>

                <th colspan="4" class="cattribute-border-left">Wild</th>

                <th colspan="4" class="cattribute-border-left">Mouth</th>

                <th colspan="4" class="cattribute-border-left">Mystery</th>

                <th colspan="4" class="cattribute-border-left">Secret</th>

                <th colspan="4" class="cattribute-border-left">Unknown</th>
            </tr>
            <tr>
                <th><a class="button is-small is-primary" v-on:click="sortIdProfile">ID</a></th>
                <th><a class="button is-small is-primary" v-on:click="sortGenProfile">Gen</a></th>
                <th><a class="button is-small is-primary" v-on:click="sortPriceProfile">Price</a></th>

                <th class="cattribute-border-left">D0</th>
                <th class="fur">R1</th>
                <th class="fur">R2</th>
                <th class="fur">R3</th>

                <th class="cattribute-border-left">D0</th>
                <th class="pattern">R1</th>
                <th class="pattern">R2</th>
                <th class="pattern">R3</th>

                <th class="cattribute-border-left">D0</th>
                <th class="eyecolor">R1</th>
                <th class="eyecolor">R2</th>
                <th class="eyecolor">R3</th>

                <th class="cattribute-border-left">D0</th>
                <th class="eyeshape">R1</th>
                <th class="eyeshape">R2</th>
                <th class="eyeshape">R3</th>

                <th class="cattribute-border-left">D0</th>
                <th class="basecolor">R1</th>
                <th class="basecolor">R2</th>
                <th class="basecolor">R3</th>

                <th class="cattribute-border-left">D0</th>
                <th class="highlightcolor">R1</th>
                <th class="highlightcolor">R2</th>
                <th class="highlightcolor">R3</th>

                <th class="cattribute-border-left">D0</th>
                <th class="accentcolor">R1</th>
                <th class="accentcolor">R2</th>
                <th class="accentcolor">R3</th>

                <th class="cattribute-border-left">D0</th>
                <th class="wild">R1</th>
                <th class="wild">R2</th>
                <th class="wild">R3</th>

                <th class="cattribute-border-left">D0</th>
                <th class="mouth">R1</th>
                <th class="mouth">R2</th>
                <th class="mouth">R3</th>

                <th class="cattribute-border-left">D0</th>
                <th class="mouth">R1</th>
                <th class="mouth">R2</th>
                <th class="mouth">R3</th>

                <th class="cattribute-border-left">D0</th>
                <th class="mouth">R1</th>
                <th class="mouth">R2</th>
                <th class="mouth">R3</th>

                <th class="cattribute-border-left">D0</th>
                <th class="mouth">R1</th>
                <th class="mouth">R2</th>
                <th class="mouth">R3</th>
            </tr>
            </thead>
            <tbody>
            <tr v-for="kitty in searchDna">
                <td><a v-bind:href="getLink(kitty.id)" target="_blank">{{ kitty.id }}</a></td>
                <td>{{ kitty.gen }}</td>
                <td>{{ kitty.sale }}</td>

                <td class="cattribute-border-left">{{ kitty['body']['D0'] }}</td>
                <td class="fur">{{ kitty['body']['R1'] }}</td>
                <td class="fur">{{ kitty['body']['R2'] }}</td>
                <td class="fur">{{ kitty['body']['R3'] }}</td>

                <td class="cattribute-border-left">{{ kitty['pattern']['D0'] }}</td>
                <td class="pattern">{{ kitty['pattern']['R1'] }}</td>
                <td class="pattern">{{ kitty['pattern']['R2'] }}</td>
                <td class="pattern">{{ kitty['pattern']['R3'] }}</td>

                <td class="cattribute-border-left">{{ kitty['eyecolor']['D0'] }}</td>
                <td class="eyecolor">{{ kitty['eyecolor']['R1'] }}</td>
                <td class="eyecolor">{{ kitty['eyecolor']['R2'] }}</td>
                <td class="eyecolor">{{ kitty['eyecolor']['R3'] }}</td>

                <td class="cattribute-border-left">{{ kitty['eyetype']['D0'] }}</td>
                <td class="eyeshape">{{ kitty['eyetype']['R1'] }}</td>
                <td class="eyeshape">{{ kitty['eyetype']['R2'] }}</td>
                <td class="eyeshape">{{ kitty['eyetype']['R3'] }}</td>

                <td class="cattribute-border-left">{{ kitty['bodycolor']['D0'] }}</td>
                <td class="basecolor">{{ kitty['bodycolor']['R1'] }}</td>
                <td class="basecolor">{{ kitty['bodycolor']['R2'] }}</td>
                <td class="basecolor">{{ kitty['bodycolor']['R3'] }}</td>

                <td class="cattribute-border-left">{{ kitty['patterncolor']['D0'] }}</td>
                <td class="highlightcolor">{{ kitty['patterncolor']['R1'] }}</td>
                <td class="highlightcolor">{{ kitty['patterncolor']['R2'] }}</td>
                <td class="highlightcolor">{{ kitty['patterncolor']['R3'] }}</td>

                <td class="cattribute-border-left">{{ kitty['secondarycolor']['D0'] }}</td>
                <td class="accentcolor">{{ kitty['secondarycolor']['R1'] }}</td>
                <td class="accentcolor">{{ kitty['secondarycolor']['R2'] }}</td>
                <td class="accentcolor">{{ kitty['secondarycolor']['R3'] }}</td>

                <td class="cattribute-border-left">{{ kitty['wild']['D0'] }}</td>
                <td class="wild">{{ kitty['wild']['R1'] }}</td>
                <td class="wild">{{ kitty['wild']['R2'] }}</td>
                <td class="wild">{{ kitty['wild']['R3'] }}</td>

                <td class="cattribute-border-left">{{ kitty['mouth']['D0'] }}</td>
                <td class="mouth">{{ kitty['mouth']['R1'] }}</td>
                <td class="mouth">{{ kitty['mouth']['R2'] }}</td>
                <td class="mouth">{{ kitty['mouth']['R3'] }}</td>

                <td class="cattribute-border-left">{{ kitty['mystery']['D0'] }}</td>
                <td class="mouth">{{ kitty['mystery']['R1'] }}</td>
                <td class="mouth">{{ kitty['mystery']['R2'] }}</td>
                <td class="mouth">{{ kitty['mystery']['R3'] }}</td>

                <td class="cattribute-border-left">{{ kitty['secret']['D0'] }}</td>
                <td class="mouth">{{ kitty['secret']['R1'] }}</td>
                <td class="mouth">{{ kitty['secret']['R2'] }}</td>
                <td class="mouth">{{ kitty['secret']['R3'] }}</td>

                <td class="cattribute-border-left">{{ kitty['unknown']['D0'] }}</td>
                <td class="mouth" >{{ kitty['unknown']['R1'] }}</td>
                <td class="mouth" >{{ kitty['unknown']['R2'] }}</td>
                <td class="mouth" >{{ kitty['unknown']['R3'] }}</td>

            </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
    import qs from 'qs';
    import axios from 'axios';

    import globalStorage from './../store';

    export default {
        name: 'dnaDashboard',
        created() {
            if (!globalStorage.state.isAuthorized) {
                this.$router.push('/');
            }
        },
        data() {
            let state = {};

            state.isSearching = false;
            state.genSort = true;
            state.price = false;
            state.idSort = true;

            state.searchResults = [];
            state.searchDna = [];

            state.cattribute = '';
            state.queryString = 'onsale=true';
            state.gen = 0;
            state.d0 = false;
            state.r1 = false;
            state.r2 = false;
            state.r3 = false;
            state.offset = 0;
            state.count = 0;

            state.dnaData = null;

            return state;
        },
        methods: {
            setupAutoComplete() {

                if (this.dnaData === null) {
                    axios.get('https://dna.cryptokittydata.info/dna/search').then(response => {
                        this.dnaData = response.data;

                        $("#cattribute").autocomplete({
                            source: this.dnaData.cattributes,
                            select: (event, ui) => {
                                this.cattribute = ui.item.value;
                            }
                        });
                    });
                }
            },
            fromWei(price) {
                return web3.fromWei(price, 'ether');
            },
            getLink(id) {
                return 'https://www.cryptokitties.co/kitty/' + id;
            },
            sortGenProfile() {
                if (this.genSort) {
                    this.searchDna.sort(this.sortProfileByGenDown);
                } else {
                    this.searchDna.sort(this.sortProfileByGenUp);
                }

                this.genSort = !this.genSort;
            },
            sortIdProfile() {
                if (this.idSort) {
                    this.searchDna.sort(this.sortProfileByIdDown);
                } else {
                    this.searchDna.sort(this.sortProfileByIdUp);
                }

                this.idSort = !this.idSort;
            },
            sortPriceProfile() {
                if (this.price) {
                    this.searchDna.sort(this.sortProfileByPriceUp);
                } else {
                    this.searchDna.sort(this.sortProfileByPriceDown);
                }

                this.price = !this.price;
            },
            sortProfileByGenUp(a, b) {
                if (a.generation > b.generation) {
                    return -1;
                } else {
                    return 1;
                }
            },
            sortProfileByGenDown(a, b) {
                if (a.generation < b.generation) {
                    return -1;
                } else {
                    return 1;
                }
            },
            sortProfileByPriceUp(a, b) {
                if (Number.parseFloat(this.fromWei(a.sale)) > Number.parseFloat(this.fromWei(b.sale))) {
                    return -1;
                } else {
                    return 1;
                }
            },
            sortProfileByPriceDown(a, b) {
                if (Number.parseFloat(this.fromWei(a.sale)) < Number.parseFloat(this.fromWei(b.sale))) {
                    return -1;
                } else {
                    return 1;
                }
            },
            sortProfileByIdUp(a, b) {
                if (Number.parseInt(a.id) > Number.parseInt(b.id)) {
                    return -1;
                } else {
                    return 1;
                }
            },
            sortProfileByIdDown(a, b) {
                if (Number.parseInt(a.id) < Number.parseInt(b.id)) {
                    return -1;
                } else {
                    return 1;
                }
            },
            appendRaw (thing, value) {
                this.queryString += '&'+thing+'='+value;
            },
            addParam () {
                //need to find what category the cattribute belongs too
                for (let category_name in this.dnaData) {
                    if (category_name !== 'cattributes') {
                        for (let cattribute in this.dnaData[category_name]) {
                            if (cattribute === this.cattribute) {
                                this.appendRaw(category_name, this.getDNAValue(this.dnaData[category_name][cattribute]));

                                return;
                            }
                        }
                    }
                }

            },
            getDNAValue (kaiCode) {
                var out = '';

                if (this.r3) {
                    out = kaiCode
                } else {
                    out = '_';
                }

                if (this.r2) {
                    out = out + kaiCode
                } else {
                    out = out + '_';
                }

                if (this.r1) {
                    out = out + kaiCode
                } else {
                    out = out + '_';
                }

                if (this.d0) {
                    out = out + kaiCode
                } else {
                    out = out + '_';
                }

                return out;
            },
            addGen (gen) {
                this.queryString += "&gen="+gen;
            },
            addReverseOrder () {
                this.queryString += "&orderingDown=yes";
            },
            search () {
                this.isSearching = true;
                this.searchDna = [];

                axios.post('https://dna.cryptokittydata.info/'+globalStorage.state.profile+'/search', qs.parse(this.queryString+"&offset="+Number.parseInt(this.offset) * 100))
                    .then(response => {
                        for (let i in response.data.results) {
                            let obj = response.data.results[i];
                            obj.id = i;
                            this.searchDna.push(obj);
                        }

                        this.count = response.data.count;
                        this.isSearching = false;
                    }).catch((err) => {
                        this.isSearching = false;
                    })
            }
        }
    }
</script>

<style>
    html {
        overflow: auto !important;
    }

    .checkbox {
        padding-right: 10px;
    }

    .cattribute-border-left {
        border-left: #0a0a0a solid 1px;
    }
</style>