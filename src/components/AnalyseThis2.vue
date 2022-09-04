<template>
<div class="analyse container-sm m-5">
    <h1>
        Text Analyzer
    </h1>
    <div class=" mb-5">
        <h2 class="mt-5">Step 1. upload enter file with terms and keys</h2>
        <label for="basic-url" class="form-label">Enter url</label>
        <div class="input-group mb-3">
            <span class="input-group-text" id="basic-addon3">URL with keys and terms</span>
            <input type="text" class="form-control" id="keys-and-terms-url" aria-describedby="basic-addon3">
        </div>
        <h2 class="mt-5">Step 2. paste text</h2>
        <p>Copy text from a webpage, a Worddoc, an E-book etc.</p>
        <textarea id="pastedText" name="pastedText" rows="5" cols="33" class="w-100 p-3"></textarea>

        <h2 class="mt-5">Step 3: Analyze</h2>
        <button @click="getURviaInput" class="btn btn-light border m-3">Analyse this!</button>
        <button class="btn btn-light mr-3 border" @click="this.clear">Clear</button>
    </div>
    <div class="results">
        <div class="row mt-3">
            <div class="col-md-12">
                <h2 class="mt-5">Output</h2>

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
                        <tr class="" v-for="entry in outputKeysAndTermsAndFrequency">
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
            <h2 class="text-center">This can take a while.</h2>
            {{ this.progressIndicator }}
        </div>
    </div>
    <canvas id="canvas"></canvas>
</div>
</template>

<script>
import * as d3 from "d3";

export default {
    name: "AnalyseThis2",
    data() {
        return {
            windowLocationOrigin: window.location.origin,
            fileName: "",
            inputTermsAndKeys: [],
            outputKeysAndTermsAndFrequency: [],
            outputKeysAndTermsAndFrequencyCreated: false,
            textAreaString: "",
            textThatNeedsToBeAnalysed: "",
            progressIndicator: "",
            loadingScreen: null,
            results: null,
            sourceURL: ""
        };
    },
    mounted() {
        this.loadingScreen = document.querySelector(".loader");
        this.results = document.querySelector(".results");
    },
    methods: {
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
                var loadingTask = pdfjsLib.getDocument(typedarray);
                that.convertPDF(loadingTask);
            };
            //Step 3:Read the file as ArrayBuffer
            fileReader.readAsArrayBuffer(file);
        },
        getURLparameters() {
            // get url with keys and terms from url parameter
            const parsedUrl = new URL(window.location.href);

            if (parsedUrl.searchParams.get("source") !== null) {
                this.sourceURL = parsedUrl.searchParams.get("source");
            }
            this.fetchTermsAndKeys(this.sourceURL);
        },
        getURviaInput() {
            const url = document.querySelector("#keys-and-terms-url").value;
            this.fetchTermsAndKeys(url);
        },

        fetchTermsAndKeys(url) {
            var that = this;
            // https://stackoverflow.com/a/60785568
            d3.dsv(" ", url).then((termsAndKeys) => {
                that.inputTermsAndKeys = termsAndKeys;
                that.getTextThatNeedsToBeAnalysedFromTextArea();
            });
        },
        getTextThatNeedsToBeAnalysedFromTextArea() {
            // put text from text area into var
            this.textThatNeedsToBeAnalysed = document.querySelector("#pastedText").value;
            this.loopThroughTerms(this.inputTermsAndKeys);
        },
        removeLineBreaks(str) {
            // remove line breaks, https://stackoverflow.com/a/10805198
            str = str.replace(/(\r\n|\n|\r)/gm, "");
        },
        createInitialOutputKeysAndTermsAndFrequency(obj) {
            var that = this;

            for (var k in obj) {
                if (obj.hasOwnProperty(k)) {
                    that.outputKeysAndTermsAndFrequency.push({
                        key: obj[k].Key,
                        term: obj[k].Term,
                        freq: 0
                    });
                }
            }
            that.outputKeysAndTermsAndFrequencyCreated = true;
        },
        loopThroughTerms(inputTermsAndKeys) {
            var that = this;

            that.removeLineBreaks(that.textThatNeedsToBeAnalysed);

            // create array with objects that contain the keys:
            if (that.outputKeysAndTermsAndFrequencyCreated === false) {
                that.createInitialOutputKeysAndTermsAndFrequency(inputTermsAndKeys);
            }

            that.textAreaString = "";
            for (let i = 0; i < inputTermsAndKeys.length; i++) {
                let count = that.textThatNeedsToBeAnalysed.split(inputTermsAndKeys[i].Term).length - 1;

                for (var k in that.outputKeysAndTermsAndFrequency) {
                    if (that.outputKeysAndTermsAndFrequency.hasOwnProperty(k)) {
                        if (inputTermsAndKeys[i].Key === that.outputKeysAndTermsAndFrequency[k].key) {
                            that.outputKeysAndTermsAndFrequency[k].freq += count;
                        }
                    }
                }
            }

            // textarea containing the text that can be copied
            for (var k in that.outputKeysAndTermsAndFrequency) {
                if (that.outputKeysAndTermsAndFrequency.hasOwnProperty(k)) {
                    that.textAreaString += that.outputKeysAndTermsAndFrequency[k].key + "," + that.outputKeysAndTermsAndFrequency[k].term + "," + that.outputKeysAndTermsAndFrequency[k].freq + "\n";
                }
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
