<template>
<!-- <div class="row d-flex justify-content-center m-5" style="max-width: 1000px;"> -->
<!-- <div class="analyse container-sm col-md-12"> -->
<div class="analyse container-sm m-5">
    <h1>
        Text Analyzer (English only)
    </h1>
    <div class=" mb-5">
        <!-- <p>If URL does not work download PDF and upload.</p> -->
        <!-- <label for="sourceURL">1: Enter URL to PDF: </label>
            <input id="sourceURL" name="sourceURL" type="text" @change="this.fetchDataUrl" />
            Or 2: -->
        <h1>Option 1. upload PDF</h1>
        <input class="btn btn-light border m-3" @change="this.fetchDataLocalFile" type="file">
        <hr>
        <h1>Option 2. paste text</h1>
        <p>Copy text from a webpage, a Worddoc, an E-book etc.</p>
        <textarea id="pastedText" name="pastedText" rows="5" cols="33" class="w-100 p-3"></textarea>
        <!-- <button @click="preparePastedText" class="btn btn-light border m-3">Analyse this!</button> -->
        <button @click="getURLparameters" class="btn btn-light border m-3">Analyse this!</button>
        <hr>
        <button class="btn btn-light mr-3 border" @click="this.clear">Clear</button>
        <button disabled @click="downloadAnalysis('analysis.txt', 'text/plain');" class="btn btn-light border m-3 downloadAnalysis">Download Analysis (testing)</button>
        <hr>
    </div>
    <div class="results">
        <h3 class="summary">This PDF ({{ fileName }}) has {{ this.numberOfPages }} pages, {{ this.numberOfSentences
                }}
            sentences and {{ this.numberOfWords }} words.</h3>
        <div class="row mt-3">
            <div class="col-md-12">
                <h2>Frequent Terms</h2>
                <p>A list of the most common terms, not based on a predefined blockchain/bitcoin related list.
                </p>
                <p class="frequentTerms wordcloud">
                    <!-- <span v-for="item in frequentTerms"><span
                                    v-bind:style="{ fontSize: (item.count/frequentTermsHighest)*100 + 'px' }"
                                    class="p-0">{{
                                    item.word }}&nbsp;&nbsp;</span></span> -->
                    <span v-for="item in frequentTerms"><span v-bind:style="{ fontSize: 20 + 'px' }" class="p-0">{{
                                item.word
                                }}&nbsp;&nbsp;</span></span>
                </p>
                <!-- <table class="mx-auto border sortable-theme-bootstrap" data-sortable>
                    <thead>
                        <tr>
                            <th data-sortable="true" class="p-2">Text string</th>
                            <th data-sortable="true" data-sorted-direction="descending" data-sortable-type="numeric" class="p-2">Count</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="item in frequentTerms">
                            <td v-bind:style="{ fontSize: item.count + 'px' }" class="p-2 border">“{{ item.word }}”</td>
                            <td class="p-2 border">{{ item.count }}</td>
                        </tr>
                    </tbody>
                </table> -->
            </div>
            <div class="col-md-12">
                <h2 class="mt-5">Configurable searches</h2>

                <!-- <p style="padding: 2em; background: #ccc;">Here comes a pie chart with the relative word count in each discriminator. Not buuild yet</p> -->

                <!-- <h2>Financed by</h2>
                    <p class=" wordcloud">
                        <span v-for="item in financedBy"><span style="" class="p-0 pr-5 border">…{{ item }}…&nbsp;&nbsp;</span></span>
                    </p> -->
                <h2>A: General Phrases and Words</h2>
                <p>Predefined text strings exactly measured:</p>
                <!-- <p>Predefined text strings exactly measured. <strong>Click on a header to sort</strong>:</p> -->
                <!-- < class=" wordcloud"> -->
                <!-- <span v-for="item in searchStrings.defaultSearchStrings"><span
                                    v-bind:style="{ fontSize: (item.count/searchStringsHighestCount.defaultSearchStrings)*100 + 'px' }"
                                    class="p-0">{{ item.string }}<sup
                                        class='itemCount'>({{item.count}})</sup>&nbsp;&nbsp;</span></span> -->

                <!-- <p v-for="item in searchStrings.defaultSearchStrings"><span v-bind:style="{ fontSize: 20 + 'px' }"
                            class="p-0">{{ item.string }} ({{ item.count }})&nbsp;&nbsp;</span>
                    </p> -->

                <table class="text-start table-primary table-striped">
                    <tr class="" v-for="item in searchStrings.defaultSearchStrings">
                        <td v-bind:style="{ fontSize: 20 + 'px' }" class="p-0">{{ item.string }}: </td>
                        <td>{{ item.count
                                }}</td>
                    </tr>
                </table>

                <p>
                    <template class="" v-for="item in searchStrings.defaultSearchStrings">
                        {{ item.string }},{{ item.count}}<br>
                    </template>
                </p>

                <!-- <h2>B: ProBitcoiners</h2>
                    <p class=" wordcloud">
                        <span v-for="item in searchStrings.proBitcoinersSearchStrings"><span
                                v-bind:style="{ fontSize: (item.count / searchStringsHighestCount.proBitcoinersSearchStrings) * 100 + 'px' }"
                                class="p-0">{{ item.string }}<sup
                                    class='itemCount'>({{ item.count }})</sup>&nbsp;&nbsp;</span></span>
                    </p>
                    <h2>C: Bullshit Phrases and Words</h2>
                    <p class=" wordcloud">
                        <span v-for="item in searchStrings.bullshitSearchStrings"><span
                                v-bind:style="{ fontSize: (item.count / searchStringsHighestCount.bullshitSearchStrings) * 100 + 'px' }"
                                class="p-0">{{ item.string }}<sup
                                    class='itemCount'>({{ item.count }})</sup>&nbsp;&nbsp;</span></span>
                    </p>
                    <h2>C: Tech Phrases and Words</h2>
                    <p class=" wordcloud">
                        <span v-for="item in searchStrings.techSearchStrings"><span
                                v-bind:style="{ fontSize: (item.count / searchStringsHighestCount.techSearchStrings) * 100 + 'px' }"
                                class="p-0">{{ item.string }}<sup
                                    class='itemCount'>({{ item.count }})</sup>&nbsp;&nbsp;</span></span>
                    </p>
                    <h2>D: Self Sovereign Identity and privacy</h2>
                    <p class=" wordcloud">
                        <span v-for="item in searchStrings.selfSovereignIdentityAndPrivacySearchStrings"><span
                                v-bind:style="{ fontSize: (item.count / searchStringsHighestCount.selfSovereignIdentityAndPrivacySearchStrings) * 100 + 'px' }"
                                class="p-0">{{ item.string }}<sup
                                    class='itemCount'>({{ item.count }})</sup>&nbsp;&nbsp;</span></span>
                    </p>
                    <h2>E: Business Phrases and Words</h2>
                    <p class=" wordcloud">
                        <span v-for="item in searchStrings.businessSearchStrings"><span
                                v-bind:style="{ fontSize: (item.count / searchStringsHighestCount.businessSearchStrings) * 100 + 'px' }"
                                class="p-0">{{ item.string }}<sup
                                    class='itemCount'>({{ item.count }})</sup>&nbsp;&nbsp;</span></span>
                    </p>
                    <h2>Financial Support</h2>
                    <p class=" wordcloud">
                        <span v-for="item in searchStrings.financialSupportSearchStrings"><span
                                v-bind:style="{ fontSize: (item.count / searchStringsHighestCount.financialSupportSearchStrings) * 100 + 'px' }"
                                class="p-0">{{ item.string }}<sup
                                    class='itemCount'>({{ item.count }})</sup>&nbsp;&nbsp;</span></span>
                    </p> -->

                <!-- <table class="mx-auto border sortable-theme-bootstrap" data-sortable>
                    <thead>
                        <tr>
                            <th data-sortable="true" class="p-2">Text string</th>
                            <th data-sortable="true" data-sorted-direction="descending" data-sortable-type="numeric" class="p-2">Count</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="item in searchStrings.businessSearchStrings">
                            <td class="p-2 border">“{{ item.string }}”</td>
                            <td class="p-2 border">{{ item.count }}</td>
                        </tr>
                    </tbody>
                </table> -->
            </div>
        </div>
        <!-- <div>
            <h2>Weight Terms</h2>
            <p>A list of the most common terms, not based on a predefined blockchain/bitcoin related list.</p>
            <table class="mx-auto border sortable-theme-bootstrap" data-sortable>
                <thead>
                    <tr>
                        <th data-sortable="true" class="p-2">Text string</th>
                        <th data-sortable="true" data-sorted-direction="descending" data-sortable-type="numeric" class="p-2">Count</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="item in weightTerms">
                        <td class="p-2 border">“{{ item.word }}”</td>
                        <td class="p-2 border">{{ item.count }}</td>
                    </tr>
                </tbody>
            </table>
        </div> -->
        <div class="text-left">
            <hr>
            <!-- <h3>Sentiment</h3> -->
            <!-- <p>{{this.sentimentAnalysis}}</p> -->
            <h2>General indicators</h2>
            <p>(not alway accurate but good for a general impression)</p>
            <h3>
                All atMentions mentioned:
            </h3>
            <p>{{ this.atMentions }}</p>
            <h3>
                All URL's mentioned:
            </h3>
            <p>{{ this.urls }}</p>
            <h3>
                All hashtags mentioned:
            </h3>
            <p>{{ this.hashTags }}</p>
            <h3>
                All emails mentioned:
            </h3>
            <p>{{ this.emails }}</p>
            <h3>
                All organisations mentioned:
            </h3>
            <p>{{ this.organisations }}</p>
            <h3>
                All acronyms mentioned:
            </h3>
            <p>{{ this.acronyms }}</p>
            <h3>
                All people mentioned:
            </h3>
            <p>{{ this.people }}</p>
            <h3>
                All places mentioned:
            </h3>
            <p>{{ this.places }}</p>
            <h3>
                All phone numbers mentioned:
            </h3>
            <p>{{ this.phoneNumbers }}</p>
            <h3>
                All emoticons mentioned:
            </h3>
            <p>{{ this.emoticons }}</p>
            <h3>
                All emojis mentioned:
            </h3>
            <p>{{ this.emojis }}</p>
            <h3>
                All money talk mentioned:
            </h3>
            <p>{{ this.money }}</p>
            <h3>
                All quotations mentioned:
            </h3>
            <p>Everything between quotes.</p>
            <p>{{ this.quotations }}</p>

            <!-- <h3>
                fff in this PDF:
            </h3> -->
            <!-- <p>{{this.sentences}}</p> -->
            <!-- <ul>
                <li v-for="item in organisations">{{item}}</li>
            </ul> -->
            <p id="content" class="text-left mt-5"></p>
            <canvas id="the-canvas"></canvas>
        </div>
    </div>
    <div class="loader">
        <div class="text-left">
            <h2 class="text-center">This can take a while, depending on size and structure of the PDF </h2>
            {{ this.progressIndicator }}
            <!-- <img src="@/assets/loading.gif" alt=""> -->
            <!-- <div class="progress">Progress: </div> -->
        </div>
    </div>
    <canvas id="canvas"></canvas>
</div>
<!-- </div> -->
</template>

<script>
// import publicPath from "../../vue.config";

// import pdfjsLib from "pdfjs-dist";
// console.log('pdfjsLib: ', pdfjsLib);

// import("pdfjs-dist").then((pdfjsLib) => {
//     console.log('pdfjsLib: ', pdfjsLib);
//     // pdfjsLib.getDocument();
// });

// https://codeutility.org/javascript-how-to-import-mozilla-pdf-js-in-vue-project-stack-overflow/
// const pdfjsLib = require("pdfjs-dist");

// import * as pdfjsLib from 'pdfjs-dist/web';

// import * as pdfjsLib from "pdfjs-dist/build/pdf";

import axios from "axios";
import * as d3 from "d3";

import * as cloud from "d3-cloud"

import nlp from "compromise";

// https://observablehq.com/@spencermountain/compromise-dates
// nlp.extend(require('compromise-dates/builds/compromise-dates.min.js'));

// https://observablehq.com/@spencermountain/compromise-sentences
nlp.extend(require('compromise-sentences/builds/compromise-sentences.min.js'));

var tm = require("text-miner");

export default {
    name: "AnalyseThis2",
    data() {
        return {
            // publicPath: publicPath.publicPath,
            windowLocationOrigin: window.location.origin,
            fileName: "",

            searchStrings: {},
            searchStringsHighestCount: {},
            index: {},
            keysAndFrequency: {}, 

            numberOfPages: 0,
            numberOfWords: 0,
            numberOfSentences: 0,
            questions: [],
            selfSovereignIdentityPrivacy: [],
            textThatNeedsToBeAnalysed: "",
            organisations: "–––",
            people: "–––",
            places: "–––",
            sentences: "–––",
            urls: "–––",
            money: "–––",
            acronyms: "–––",
            phoneNumbers: "–––",
            hashTags: "–––",
            emails: "–––",
            emoticons: "–––",
            emojis: "–––",
            atMentions: "–––",
            quotations: "–––",
            frequentTerms: [],
            frequentTermsHighest: 0,
            weightTerms: [],
            sentimentAnalysis: {},
            progressIndicator: "",
            financedBy: [],

            // loadingscreen
            loadingScreen: null,
            results: null,
            downloadAnalysisButton: null,
            sourceURL: ""
            // end loadingscreen

        };
    },
    mounted() {
        // import("pdfjs-dist").then((pdfjsLib) => {
        //     console.log('pdfjsLib: ', pdfjsLib);
        //     // pdfjsLib.getDocument();
        // });
        this.defineLoadingScreen();
        // this.getURLparameters();
    },
    methods: {
        defineLoadingScreen() {
            this.loadingScreen = document.querySelector(".loader");
            this.results = document.querySelector(".results");
            this.downloadAnalysisButton = document.querySelector(".downloadAnalysis");
        },
        turnLoadingScreenOn() {
            console.log('this.loadingScreen: ', this.loadingScreen);
            this.loadingScreen.classList.add("loading");
        },
        turnLoadingScreenOff() {
            this.downloadAnalysisButton.disabled = false;
            this.loadingScreen.classList.remove("loading");
            this.results.style.display = "block";
        },
        downloadAnalysis(fileName, contentType) {
            var a = document.createElement("a");
            var file = new Blob([this.numberOfPages, ",", this.numberOfWords, ",", this.frequentTerms], {
                type: contentType
            });
            a.href = URL.createObjectURL(file);
            a.download = fileName;
            a.click();
        },
        findHighestInFrequentTerms(array, key) {
            // To find the maximum y value of the objects in array:
            this.frequentTermsHighest = Math.max.apply(Math, array.map(function (o) {
                return o[key];
            }));
        },
        findHighestInSearchStrings(a) {
            this.searchStringsHighestCount[a] = Math.max.apply(Math, this.searchStrings[a].map(function (o) {
                return o.count;
            }));
        },
        getSearchStringInArray(a) {
            // make array from what is in the text field (which may be populated with what is in localStorage). Cannot be used in mounted(), that is too early.
            return document.querySelector("#" + a).value.split(","); // split turns string into array
        },
        clear() {
            window.location = window.location;
        },
        analyse() {
            var that = this;
            this.getURLparameters();

            for (let i = 0; i < that.getSearchStringInArray("defaultSearchStrings").length; i++) {
                that.countSpecificStrings(that.getSearchStringInArray("defaultSearchStrings")[i], "defaultSearchStrings");
            }

            /**
             * REMOVE LOADING SCREEN
             */
            console.log("ready");
            that.progressIndicator += " ready";

            that.turnLoadingScreenOff();
            // setTimeout(() => {
            //     that.turnLoadingScreenOff();
            // }, 1);
        },
        createIndexOfTerms() {

            /**
             * REMOVE LOADING SCREEN
             */
            console.log("ready");
            that.progressIndicator += " ready";

            that.turnLoadingScreenOff();
            // setTimeout(() => {
            //     that.turnLoadingScreenOff();
            // }, 1);
        },
        preparePastedText() {
            this.turnLoadingScreenOn();

            // this has to be in a separate “thread” else the loading screen showing will be delayed so it becomes useless
            setTimeout(() => {
                this.textThatNeedsToBeAnalysed = document.querySelector("#pastedText").value;
                this.analyse();
            }, 100);
        },

        countSpecificStrings(string, targetKey) {
            // structure:
            // searchStrings = {
            //   defaultSearchStrings: [{
            //       a: 1,
            //       b: 2
            //     },
            //     {
            //       a: 1,
            //       b: 2
            //     }
            //   ],
            //   businessSearchStrings: [{
            //     a: 3,
            //     b: 2
            //   }]
            // };
            // https://stackoverflow.com/a/17886301
            var stringToGoIntoTheRegex = string;
            var regex = new RegExp("" + stringToGoIntoTheRegex + "", "gi");
            var count = (this.textThatNeedsToBeAnalysed.match(regex) || []).length;
            if (this.searchStrings[targetKey] === undefined) {
                this.searchStrings[targetKey] = [];
            }
            if (count > 0) { // only if there is at least one occurance it should be stored
                this.searchStrings[targetKey].push({
                    "string": string,
                    "count": count
                });
            }
        },
        createIndex(string, targetKey) {
            // structure:
            // searchStrings = {
            //   defaultSearchStrings: [{
            //       a: 1,
            //       b: 2
            //     },
            //     {
            //       a: 1,
            //       b: 2
            //     }
            //   ],
            //   businessSearchStrings: [{
            //     a: 3,
            //     b: 2
            //   }]
            // };
            // https://stackoverflow.com/a/17886301
            var stringToGoIntoTheRegex = string;
            var regex = new RegExp("" + stringToGoIntoTheRegex + "", "gi");
            var count = (this.textThatNeedsToBeAnalysed.match(regex) || []).length;
            if (this.searchStrings[targetKey] === undefined) {
                this.searchStrings[targetKey] = [];
            }
            if (count > 0) { // only if there is at least one occurance it should be stored
                this.searchStrings[targetKey].push({
                    "string": string,
                    "count": count
                });
            }
        },

        fetchDataLocalFile(e) {
            var that = this;
            var pageNrCounter = 1;
            var file = e.target.files[0];
            this.fileName = e.target.files[0].name;

            // https://stackoverflow.com/a/28567893
            //Step 2: Read the file using file reader
            var fileReader = new FileReader();

            fileReader.onload = function () {
                //Step 4:turn array buffer into typed array
                var typedarray = new Uint8Array(this.result);
                console.log('pdfjsLib: ', pdfjsLib);
                var loadingTask = pdfjsLib.getDocument(typedarray);
                that.convertPDF(loadingTask);
            };
            //Step 3:Read the file as ArrayBuffer
            fileReader.readAsArrayBuffer(file);
        },
        fetchDataUrl(e) { //TODO: rename to make clear that it's only pdf
            var that = this;
            var content = document.querySelector("#content");

            // https://mozilla.github.io/pdf.js/api/draft/module-pdfjsLib.html
            // pdfjsLib.getDocument('https://atrium.uninnovation.network/guide');

            // https://medium.com/data-scraper-tips-tricks/scraping-data-with-javascript-in-3-minutes-8a7cf8275b31
            // https://www.npmjs.com/package/puppeteer
            // https://medium.com/@bretcameron/how-to-build-a-web-scraper-using-javascript-11d7cd9f77f2
            // https://stackoverflow.com/a/20522307
            // https://mozilla.github.io/pdf.js/examples/
            // https://davidwalsh.name/fetch

            var loadingTask = pdfjsLib.getDocument(e.target.value);

            var pageNrCounter = 1;
            // var textThatNeedsToBeAnalysed = "";

            that.convertPDF(loadingTask);
        },
        getURLparameters() {
            const parsedUrl = new URL(window.location.href);
            // const strAllQueryParameters = window.location.search;
            // const allQueryParameters = new URLSearchParams(strAllQueryParameters);

            if (parsedUrl.searchParams.get("source") !== null) {
                this.sourceURL = parsedUrl.searchParams.get("source");
            }
            this.fetchTermsAndKeys(this.sourceURL);
        },
        fetchTermsAndKeys(url) {
            // https://stackoverflow.com/a/60785568
            d3.dsv(" ", url).then((termsAndKeys) => {
                this.loopThroughTerms(termsAndKeys);
            });
        },
        getTextThatNeedsToBeAnalysedFromTextArea() { 
            // put text from text area into var
            this.textThatNeedsToBeAnalysed = document.querySelector("#pastedText").value;

        },
        removeLineBreaks(str) { 
            // remove line breaks
            str = str.replace(/(\r\n|\n|\r)/gm, "");

        },
        loopThroughTerms(termsAndKeys) {
            var that = this;

            that.getTextThatNeedsToBeAnalysedFromTextArea();


            // remove line breaks, https://stackoverflow.com/a/10805198
            that.removeLineBreaks(that.textThatNeedsToBeAnalysed);

            console.log('termsAndKeys.length: ', termsAndKeys.length);
            for (let i = 0; i < termsAndKeys.length; i++) {

                console.log('termsAndKeys[i]: ', termsAndKeys[i].Term);
                that.textThatNeedsToBeAnalysed.indexOf(termsAndKeys[i].Term) !== -1; // true
                console.log('that.textThatNeedsToBeAnalysed.indexOf(termsAndKeys[i].Term) !== -1: ', that.textThatNeedsToBeAnalysed.indexOf(termsAndKeys[i].Term) !== -1);

            }

            // for (let i = 0; i < that.getSearchStringInArray("defaultSearchStrings").length; i++) {
            //     that.countSpecificStrings(that.getSearchStringInArray("defaultSearchStrings")[i], "defaultSearchStrings");
            // }

        }

    }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->

<style lang="scss" scoped>
h3 {
    margin: 40px 0 0;
}

ul {
    list-style-type: none;
    padding: 0;
}

li {
    display: inline-block;
    margin: 0 10px;
}

a {
    color: #42b983;
}

.loader {
    display: none;
}

.loader.loading {
    display: block;
    background: rgba(34, 34, 34, 0.747);
    width: 100%;
    height: 100%;
    position: fixed;
    top: 0;
    left: 0;
    // pointer-events: none;
    color: #eee;

    // display: flex;
    // justify-content: center;
    // align-items: center;

}

.loader .progress {
    color: #222;
    background: #eee;
    ;
    height: 100%;
    min-height: 200px;
    border: 3px solid #900;
}

.loader img {
    width: 50px;
    display: block;
}

// .wordcloud {
//     background: rgba(34, 34, 34, 0.055);
//     padding: 4em 1em;
// }

// .wordcloud span span {
//     // border: none;
//     line-height: 0.2;
//     color: rgba(34, 34, 34, 0.568);
// }

// .wordcloud:hover span span {
//     font-size: 30px !important;
//     transition: all 1s ease-in-out;
//     // background: red;
// }

// .wordcloud span span {
//     font-size: auto !important;
//     transition: all 1s ease-in-out;
//     // background: red;
// }

.summary {
    background: rgba(34, 34, 34, 0.048);
    padding: 1em;
}

.results {
    display: none;
}

sup.itemCount {
    // font-size: 15px;
    font-size: 1.3em;
    display: inline-block;
    margin-top: -5.5em;
    margin-left: -0.2em;
}
</style>
