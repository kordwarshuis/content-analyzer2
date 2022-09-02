<template>
<div class="analyse container-sm m-5">
    <h1>
        Text Analyzer (English only)
    </h1>
    <div class=" mb-5">
        <h1>Option 1. upload PDF</h1>
        <input class="btn btn-light border m-3" @change="this.fetchDataLocalFile" type="file">
        <hr>
        <h1>Option 2. paste text</h1>
        <p>Copy text from a webpage, a Worddoc, an E-book etc.</p>
        <textarea id="pastedText" name="pastedText" rows="5" cols="33" class="w-100 p-3"></textarea>
        <button @click="getURLparameters" class="btn btn-light border m-3">Analyse this!</button>
        <hr>
        <button class="btn btn-light mr-3 border" @click="this.clear">Clear</button>

        <hr>
    </div>
    <div class="results">
        <div class="row mt-3">
            <div class="col-md-12">
                <h2 class="mt-5">Output</h2>

                <!-- test1 -->
                <h3>CSV, select and copy</h3>
                <textarea name="" id="" cols="30" rows="10" v-html="textAreaString"></textarea>

                <h3>In tableform</h3>
                <table class="text-start table table-striped table-bordered table-responsive">
                    <thead>
                        <tr>
                            <th scope="col">Key</th>
                            <th scope="col">Term</th>
                            <th scope="col">Freq.</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr class="" v-for="entry in keysAndTermsAndFrequency">
                            <td>{{ entry.key }}</td>
                            <td>{{ entry.term }}: </td>
                            <td>{{ entry.freq }}</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>

    </div>
    <div class="loader">
        <div class="text-left">
            <h2 class="text-center">This can take a while, depending on size and structure of the PDF </h2>
            {{ this.progressIndicator }}
        </div>
    </div>
    <canvas id="canvas"></canvas>
</div>
<!-- </div> -->
</template>

<script>
import * as d3 from "d3";

export default {
    name: "AnalyseThis2",
    data() {
        return {
            windowLocationOrigin: window.location.origin,
            fileName: "",
            keysAndTermsAndFrequency: [],
            textAreaString: "",
            textThatNeedsToBeAnalysed: "",
            urls: "–––",
            progressIndicator: "",

            loadingScreen: null,
            results: null,
            downloadAnalysisButton: null,
            sourceURL: ""
        };
    },
    mounted() {
        this.defineLoadingScreen();
    },
    methods: {
        defineLoadingScreen() {
            this.loadingScreen = document.querySelector(".loader");
            this.results = document.querySelector(".results");
            this.downloadAnalysisButton = document.querySelector(".downloadAnalysis");
        },
        turnLoadingScreenOff() {
            this.loadingScreen.classList.remove("loading");
            this.results.style.display = "block";
        },
        clear() {
            window.location = window.location;
        },
        fetchDataLocalFile(e) {
            var that = this;
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
        getURLparameters() {
            const parsedUrl = new URL(window.location.href);

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
            // remove line breaks, https://stackoverflow.com/a/10805198
            str = str.replace(/(\r\n|\n|\r)/gm, "");
        },
        loopThroughTerms(termsAndKeys) {
            var that = this;

            that.getTextThatNeedsToBeAnalysedFromTextArea();

            that.removeLineBreaks(that.textThatNeedsToBeAnalysed);

            for (let i = 0; i < termsAndKeys.length; i++) {
                // https://stackabuse.com/javascript-how-to-count-the-number-of-substring-occurrences-in-a-string/ :
                let count = that.textThatNeedsToBeAnalysed.split(termsAndKeys[i].Term).length - 1;
                that.keysAndTermsAndFrequency.push({
                    "term": termsAndKeys[i].Term,
                    "key": termsAndKeys[i].Key,
                    "freq": count
                });

                that.textAreaString += termsAndKeys[i].Term + "," + termsAndKeys[i].Key + "," + count;
            }
            that.turnLoadingScreenOff();
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
    color: #eee;
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
