<template>
<div id="menu-and-buttons-wrapper">
    <div class="menu-wrap">
        <div class="content">
            <h1>Configuration</h1>
            <p>Fields contain a default set of words and phrases. You can add / remove as you wish and save this
                (local, on your computer). You can also reset back to the default set.</p>
            <p><strong>Case insensitive. Spaces at the beginning and end also count. <code>[…], PoW ,[…]</code>only
                    gives pow; <code>[…],PoW,[…]</code> also gives “power”.</strong></p>

            <h2 class="mt-5">A. General Phrases and Words</h2>
            <p>Typical words and sentences used in a Bitcoin context.</p>
            <textarea id="defaultSearchStrings" name="defaultSearchStrings" rows="5" cols="33" class="w-100 p-3">-sequences/,ACDC,ADC,agency,agent,AID,ambient-verifiability,AN,APC,append-only-event-logs,authentic-chained-data-container,authentic-data-container,authentic-provenance-chain,authenticity,authoritativeautonomic-computing-systems,autonomic-identifier,autonomic-identity-system,autonomic-namespace,BADA,base64,best-available-data-acceptance-mechanism,BFT,binding,blake3,branch,byzantine-agreement,byzantine-fault-tolerance,certificate-transparency,CESR,cesr-proof-signatures,chain-of-custody,claim,clone,cloud-agent,composable-event-streaming-representation,configuration-files,consensus-mechanism,content-addressable-hash,control-authority,controller,coroutines,correlation,credential,crypto-libraries,cryptocurrency,cryptographic-commitment-scheme,cryptographic-strength,cryptonym,CT,DAG,data-anchor,decentralized-identity,decentralized-key-management-infrastructure,DEL,delegated-identifier,delegation,delegation,derivation-code,DHT,digest,digital-signature,directed-acyclic-graph,distributed-hash-table,DKMI,DPKI,dual-text-binary-encoding-format,duplicitous-event-log,duplicity,electronic-signature,emory-Mapped_Database,end-verifiable,entropy,ephemeral,escrow-state,establishment-event,first-seen,gnu-privacy-guard,GPG,habery,hierarchical-asynchronous-coroutines-and-input-output,hio,I-O,IANA,identifier,identifier-system,identity,inception,inception-event,inconsistency,indexed-signature,indexed-signature ,input-output,inquisitor,interaction-event,internal-inconsistency,internet-assigned-numbers-authority,ip-address,IPEX,issuance-and-presentation-exchange-protocol,issuance-event,javascript-object-signing-and-encryption,JOSE,judge,KA2CE,KAACE,keep,KEL,KERI,keri-agreement-algorithm-for-control-establishment,keri-command-line-interface,keri-improvement-doc,keridemlia,KERL,key,key-compromise,key-event,key-event-log,key-event-message,key-event-receipt,key-event-receipt-infrastructure,key-event-receipt-log,key-management,key-state,key-stretching,key-transparency,keystore,KID,kli,ledger-backer,levels-of-assurance,liveness,LoA,LoC,loci-of-control,locked-state,management-transaction-event-log,message,multicodec,multisig,namespace,nested-cooperative-delegated-identifiers,NFT,non-establishment-event,non-fungible-token,non-normative,non-repudiable,non-transferable,non-transferable-identitifer,normative,one-way-functions,OOBI,out-of-band-introduction,out-of-band-introduction,P2P,passcode,payload,peer-to-peer,PGP,PKI,pre-rotation,prefix,"pretty-good-privacy",primary-root-of-trust,primitive,proof-of-authority,proof-of-authorship,provenance,PTEL,public-key-infrastructure,public-transaction-event-log,public-verifiable-credential-registry,qualified,race-condition,ransfer_Protocol,receipt,receipt-log,registrar,repo,revocation-event,root-of-trust,rotation,rotation-event,SAD,SAID,salt,SATP,SCID,seal,secondary-root-of-trust,secure-asset-transfer-protocol,secure-attribution,seed,self-addressing-data,self-addressing-identifier,self-certifying-identifier,self-framing,self-sovereign-identity,server-sent-event,service-endpoint,signed-digest,signing-threshold,single-signature-identifier,spanning-layer,SSI,ssi-system,sub-shell,TCP,tcp-endpoint,TEL,text-binary-concatenation-composability,threshold-signature-scheme,transaction-event-log,transfer-off-ledger,transferable-identifier,transmission-control-protocol,trust-domain,UI,uniform-resource-locator,URL,user-interface,validator,VC,VC-TEL,VDS,veracity,verifiable,verifiable-credential,verifiable-data-structure,verifiable-legal-entity-identifier,verifier,verify-signature,verify-signature,version,virtual-credential-transaction-event-log,wallet,watcher,web-of-trust,well-known witnesses,witness,witness,zero-trust</textarea>
            <button @click="saveSearchStringToLocalStorage('defaultSearchStrings')" type="button" class="btn btn-light mr-2">Save</button>
            <button @click="resetSearchString('defaultSearchStrings')" type="button" class="btn btn-light mr-2">Reset</button>

            <h2 class="mt-5">B. proBitcoiners</h2>
            <p>List of people who are pro Bitcoin.</p>
            <textarea id="proBitcoinersSearchStrings" name="proBitcoinersSearchStrings" rows="5" cols="33" class="w-100 p-3">@aantonop,Andreas Antonopoulos,@AaronvanW,Aaron van Wirdum,@adam3us,@AkinSawyerr,@APompliano,Pompliano,@AskBlockchain,@BC_Stories,@bitcoincoreorg,@BitcoinMagazine,@bitstein,Michael Goldstein,@blockchain,@BlockchainTalkz,@btconometrics,@CaitlinLong_,Caitlin Long,@coincenter,@CoinDesk,@Cointelegraph,@crypto,@Crypto_Scam,@crypto_voices,@CryptoMichNL,@cryptotrader_nl,@cz_binance,@danheld,Dan Held,@DeCryptonauten,@eric_lombrozo,Eric Lombrozo,@ErikVoorhees,Erik Voorhees,@Excellion,@francispouliot_,@giacomozucco,Giacomo Zucco,@gladstein,Alex Gladstein,@goTenna,@hodlhodl,@jimmysong,Jimmy Song,@JoeSquawk,@krugermacro,@LittleBitcoinBk,@lopp,Jameson Lopp,@marcvanderchijs,Marc van der Chijs,@MartyBent,Marty Bent,@MattAhlborg,@maxkeiser,Max Keiser,@MustStopMurad,@nic__carter,Nic Carter,@NickSzabo4,Nick Szabo,@OdysseyMomentum,@pamelawjd,Pamela Morgan,@peterktodd,Peter Todd,@PeterMcCormack,Peter McCormack,@PeterSchiff,@pierre_rochard,Pierre Rochard,@provoost,@rutgervz,@saifedean,Saifedean Ammous,@skwp,@stephanlivera,Stephan Livera,@TheBitcoinNews,@TheLTBNetwork,@TobiasAHuber,@TuurDemeester,Tuur Demeester,@twiet,@valkenburgh,Peter Van Valkenburgh,@VitalikButerin,@WhalePanda,@WvNoort,@Xentagz,@ydemombynes</textarea>
            <button @click="saveSearchStringToLocalStorage('proBitcoinersSearchStrings')" type="button" class="btn btn-light mr-2">Save</button>
            <button @click="resetSearchString('proBitcoinersSearchStrings')" type="button" class="btn btn-light mr-2">Reset</button>

            <h2 class="mt-5">C. Bullshit Phrases and Words</h2>
            <p>Common Bullshit used in a Bitcoin and Blockchain context.</p>
            <textarea id="bullshitSearchStrings" name="bullshitSearchStrings" rows="5" cols="33" class="w-100 p-3"> Smart blockchain,Request Network, REQ ,Nxt ,Syscoin ,Deep Brain Chain, DBC ,EnjinCoin, ENJ , SONM , SNM ,Streamr DAT Acoin ,Ripio Credit, RCN ,Simple Token, OST ,Etherparty, FUEL,Tierion, TNT ,Coin Dash, CDT ,YOYOW,Viberate, VIB ,Snovio,SNOV ,QWARK</textarea>
            <button @click="saveSearchStringToLocalStorage('bullshitSearchStrings')" type="button" class="btn btn-light mr-2">Save</button>
            <button @click="resetSearchString('bullshitSearchStrings')" type="button" class="btn btn-light mr-2">Reset</button>

            <h2 class="mt-5">C. Technical</h2>
            <!-- <p>Common Bullshit used in a Bitcoin and Blockchain context.</p> -->
            <textarea id="techSearchStrings" name="techSearchStrings" rows="5" cols="33" class="w-100 p-3"> ASIC , BIP , ECDSA , hash , p2p , pool , PoS , pow , txid ,51% attack,ASIC,Block explorer,Block height,Block reward,Block size limit,Block subsidy,Block validation,Byzantine,Censorship-resistant,CHECKSIG,Cold wallet,Consensus,Consensus fork,Distributed Ledger,Double spending,Finney attack,Flood attack,Full node,Halving,Hard Fork,Hash tree,Hashrate,HODL,Hot wallet,Immutability,Mempool,Merged mining,Merkle branch,Merkle hash,Merkle root,Merkle tree ,Micropayment,Mining,Nakamoto consensus,Network confirmation,Network latency,nLockTime,Node,Nonce,Normalized Transaction ID,nSequence,Off-chain,On-chain,Orphan rate,Orphaned block,Peer-to-peer,Private key,Proof of stake,proof of work,Proof-of-stake,proof-of-work,Propagation,Pseudo-random,Public key,Relative lock time,Replace-by-fee,RIPEMD160,Schism hardfork,Segregated witness,SegWit,Selfish mining,SHA256,Sidechain,Signature,Smart Property,Soft fork,Softfork,Solidity,Sybil attack,Timestamp,Token,Transaction fee,transformative technology,Tree-chain,Unilateral softfork,Unspent Transaction Output,UTXO,UTXO commitment,Validation-cost metric,Zero-confirmation transaction,Zero-knowledge proofs</textarea>
            <button @click="saveSearchStringToLocalStorage('techSearchStrings')" type="button" class="btn btn-light mr-2">Save</button>
            <button @click="resetSearchString('techSearchStrings')" type="button" class="btn btn-light mr-2">Reset</button>

            <h2 class="mt-5">D. Self Sovereign Identity and privacy</h2>
            <p>Everything related to privacy, self sovereign identity.</p>
            <textarea id="selfSovereignIdentityAndPrivacySearchStrings" name="selfSovereignIdentityAndPrivacy" rows="5" cols="33" class="w-100 p-3">AML,Augmented Social Network,biometrics,centralized authorities,centralized entities,CFT,Continental Identity models,decentralized model,digital identity,Everynym,federated identity,free,free,GPDR,human identity,identity technology,KYC,legal identities,mathematical policy,OpenID,own,persistent online identity,privacy,Scandinavian Identity models,self sovereign,Self Sovereign Identity,self-sovereign identity,single authority,single authority,social graph,state-issued credentials,transparent,user-centric identity,Web of Trust,Windhover Principles</textarea>
            <button @click="saveSearchStringToLocalStorage('selfSovereignIdentityAndPrivacySearchStrings')" type="button" class="btn btn-light mr-2">Save</button>
            <button @click="resetSearchString('selfSovereignIdentityAndPrivacySearchStrings')" type="button" class="btn btn-light mr-2">Reset</button>

            <h2 class="mt-5">E. Business Phrases and Words</h2>
            <p>Phrases often used in a business context.</p>
            <textarea id="businessSearchStrings" name="businesSearchStrings" rows="5" cols="33" class="w-100 p-3">  DLT ,  ERP ,  ROI , accelerate, added security, blockchain as a , blockchain ecosystem, blockchain journey, business benefits, business challenges, business operations, business opportunities, business outcomes, business to business, business world, changing business, changing the world, co-create, commercialize, competitive advantages, corporate bond transfers, customer engagement, decentralized identity layer, disruptions, distributed ledger technology, dramatically, ECerts , enrollment certificates, enterprise applications, enterprise blockchain platforms, era of trust, governance, growth, hyperconnected, markets, maximize, multicloud, opportunities, optimized for blockchain, permissioned blockchain, pools of liquidity, reliable, risk factors, smart contracts, smarter enterprises, stakeholders, success stories, traceable, turnaround time, validate,blockchain journey,blockchain transformation,business opportunities,digital transformation,enterprise solution,leading the business,smart blockchain,smarter enterprises,transformative technology,visionary companies</textarea>
            <button @click="saveSearchStringToLocalStorage('businessSearchStrings')" type="button" class="btn btn-light mr-2">Save</button>
            <button @click="resetSearchString('businessSearchStrings')" type="button" class="btn btn-light mr-2">Reset</button>

            <h2 class="mt-5">Financial Support</h2>
            <!-- <p>Phrases often used in a business context.</p> -->
            <textarea id="financialSupportSearchStrings" name="financialSupportSearchStrings" rows="5" cols="33" class="w-100 p-3">we thank our,sponsored by,was made possible by,donation,financial contribution,financial support,very appreciative,very fortunate,really grateful,incredibly grateful,highly grateful</textarea>
            <button @click="saveSearchStringToLocalStorage('financialSupportSearchStrings')" type="button" class="btn btn-light mr-2">Save</button>
            <button @click="resetSearchString('financialSupportSearchStrings')" type="button" class="btn btn-light mr-2">Reset</button>
            <hr class="m-5">
        </div>
    </div>

    <input type="checkbox" id="open-button" />
    <label class="menuicon " for="open-button">
        <span></span>
        <span class="visuallyhidden">Open/Close Menu</span>
    </label>

</div>
</template>

<script>
export default {
    name: "MenuMain",
    data() {
        return {
            // defaultSearchStrings: "",
            // techSearchStrings: "",
            // proBitcoinersSearchStrings: "",
            // selfSovereignIdentityAndPrivacySearchStrings: "",
            // bullshitSearchStrings: "",
            // businessSearchStrings: "",
            // financialSupportSearchStrings: ""
            searchStrings: []
        }
    },
    mounted: function () {
        // take the default content of the textarea and safe it an array so we can always reset
        this.searchStrings.defaultSearchStrings = document.querySelector("#defaultSearchStrings").value,
        this.searchStrings.techSearchStrings = document.querySelector("#techSearchStrings").value,
        this.searchStrings.proBitcoinersSearchStrings = document.querySelector("#proBitcoinersSearchStrings").value,
        this.searchStrings.selfSovereignIdentityAndPrivacySearchStrings = document.querySelector("#selfSovereignIdentityAndPrivacySearchStrings").value,
        this.searchStrings.bullshitSearchStrings = document.querySelector("#bullshitSearchStrings").value,
        this.searchStrings.businessSearchStrings = document.querySelector("#businessSearchStrings").value,
        this.searchStrings.financialSupportSearchStrings = document.querySelector("#financialSupportSearchStrings").value,

        // // get the content from LocalStorage
        this.getSearchStringFromLocalStorage("defaultSearchStrings");
        this.getSearchStringFromLocalStorage("techSearchStrings");
        this.getSearchStringFromLocalStorage("proBitcoinersSearchStrings");
        this.getSearchStringFromLocalStorage("selfSovereignIdentityAndPrivacySearchStrings");
        this.getSearchStringFromLocalStorage("bullshitSearchStrings");
        this.getSearchStringFromLocalStorage("businessSearchStrings");
        this.getSearchStringFromLocalStorage("financialSupportSearchStrings");
    },
    methods: {
        // https://stackoverflow.com/a/34156339
        // download(jsonData, 'json.txt', 'text/plain');
        download(content, fileName, contentType) {
            var content1 = document.querySelector(content).value;
            var a = document.createElement("a");
            var file = new Blob([content1], {
                type: contentType
            });
            a.href = URL.createObjectURL(file);
            a.download = fileName;
            a.click();
        },
        // save the textarea content (that the user may have changed) to LocalStorage
        saveSearchStringToLocalStorage(a) {

            console.log(document.querySelector("#" + a).value);

            localStorage.setItem(a, document.querySelector("#" + a).value);
            // this.$store.commit("showToast", "Searchstrings are saved on this computer.");
            console.log("Searchstrings are saved on this computer.");
            console.log(localStorage.getItem(a));
        },
        resetSearchString(a) {
            // localStorage.setItem(a, document.querySelector("#" + a).value);
            // this.$store.commit("showToast", "Searchstrings are saved on this computer.");
            // document.querySelector("#" + a).value = localStorage.getItem(a);
            // document.querySelector("#" + a).value = this.$store.state.searchStrings[a];

            document.querySelector("#" + a).value = this.searchStrings[a];

            localStorage.setItem(a, document.querySelector("#" + a).value);

            // this.$store.commit("showToast", "Searchstrings are resetted.");
            console.log("Searchstrings are resetted.");

        },
        getSearchStringFromLocalStorage(a) {
            if (localStorage.getItem(a) !== null) {
                document.querySelector("#" + a).value = localStorage.getItem(a);
            }
        }
    }
};

/**
 * Licensed under the MIT license.
 * http://www.opensource.org/licenses/mit-license.php
 * 
 * Copyright 2014, Codrops
 * http://www.codrops.com
 * 
 * Adapted by Kor Dwarshuis
 */

// TIP: open menu initially by adding this class to body: show-menu, and set isOpen = true;
function sideMenu() {
    'use strict';
    var bodyEl = document.body,
        // app = document.querySelector('#app'),
        openbtn = document.getElementById('open-button'),
        isOpen = false,
        navMenuItems = document.querySelectorAll("a");

    function initEvents() {
        openbtn.addEventListener('click', toggleMenu);
    }

    function toggleMenu() {
        if (isOpen) {
            bodyEl.classList.remove('show-menu');
        } else {
            bodyEl.classList.add('show-menu');
        }
        isOpen = !isOpen;
    }

    function toggleMenuFromNav() {
        toggleMenu();

        // if the input isnt clicked but menu is toggled anyway, then we have to remove checked=true also
        openbtn.checked = false;
    }

    for (let i = 0; i < navMenuItems.length; i++) {
        navMenuItems[i].addEventListener("click", toggleMenuFromNav, false);
    }

    initEvents();
}

document.addEventListener("DOMContentLoaded", function () {
    sideMenu();
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->

<style lang="scss" scoped>
/* ACCESSIBILITY */
.visuallyhidden {
    border: 0;
    clip: rect(0 0 0 0);
    height: 1px;
    margin: -1px;
    overflow: hidden;
    padding: 0;
    position: absolute;
    width: 1px;
}

/* MENU
* https://tympanus.net/codrops/2014/09/16/off-canvas-menu-effects/ 
* source: Codrops
*/
#menu-and-buttons-wrapper {
    margin: 0;
    margin-left: -1em; // compensate for bootstrap grid
    padding: 0;
}

.colorshield {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    // pointer-events: none;
    opacity: 1;
}

.menu-wrap {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    margin: 0;
    padding: 0;
    text-align: left;
    background-size: cover;
    transform: translate3d(-100%, 0, 0);
    transition: transform 0.4s;
    transition-timing-function: cubic-bezier(0.7, 0, 0.3, 1);
    box-shadow: 0px 0px 37px 0px rgba(0, 0, 0, 0.75);
}

// makes slide in menu vertical scrollable
.content {
    height: 100%;
    width: 100%;
    padding: 2.5em 1.5em 0;
    overflow: scroll;
}

/* Animation of menu */
.show-menu .menu-wrap {
    transform: translate3d(0, 0, 0);
    transition: transform 0.4s;
    transition-timing-function: cubic-bezier(0.7, 0, 0.3, 1);
}

/* HAMBURGER MENU 
 * https://codepen.io/perjor/pen/yOzZPj
 *
 */
#open-button {
    display: none;
}

.menuicon {
    position: fixed;
    top: 10px;
    left: 10px;
    display: block;
    cursor: pointer;
    height: 21px;
    width: 25px;
    z-index: 5;
}

.menuicon>span:first-child,
.menuicon>span:first-child::after,
.menuicon>span:first-child::before {
    display: block;
    width: 22px;
    height: 3px;
    border-radius: 15px;
    background-color: #000;
}

.menuicon>span:first-child {
    top: 8px;
    position: relative;
    -webkit-transition-duration: 0;
    -moz-transition-duration: 0;
    -ms-transition-duration: 0;
    -o-transition-duration: 0;
    -webkit-transition-delay: 0.2s;
    -moz-transition-delay: 0.2s;
    -ms-transition-delay: 0.2s;
    -o-transition-delay: 0.2s;
    transition-delay: 0.2s;
}

.menuicon>span:first-child::after,
.menuicon>span:first-child::before {
    content: '';
    position: absolute;
    -webkit-transition-property: margin, -webkit-transform;
    -webkit-transition-duration: 0.2s;
    -moz-transition-duration: 0.2s;
    -ms-transition-duration: 0.2s;
    -o-transition-duration: 0.2s;
    transition-duration: 0.2s;
    -webkit-transition-delay: 0.2s;
    -moz-transition-delay: 0.2s;
    -ms-transition-delay: 0.2s;
    -o-transition-delay: 0.2s;
    transition-delay: 0.2s;
}

.menuicon>span:first-child::before {
    margin-top: -8px;
}

.menuicon>span:first-child::after {
    margin-top: 8px;
}

#open-button:checked~.menuicon>span:first-child {
    background-color: transparent;
}

#open-button:checked~.menuicon>span:first-child::before,
#open-button:checked~.menuicon>span:first-child::after {
    margin-top: 0px;
}

#open-button:checked~.menuicon>span:first-child::before {
    -webkit-transform: rotate(45deg);
    -moz-transform: rotate(45deg);
    -ms-transform: rotate(45deg);
    -o-transform: rotate(45deg);
    transform: rotate(45deg);
}

#open-button:checked~.menuicon>span:first-child::after {
    -webkit-transform: rotate(-45deg);
    -moz-transform: rotate(-45deg);
    -ms-transform: rotate(-45deg);
    -o-transform: rotate(-45deg);
    transform: rotate(-45deg);
}

/* END HAMBURGER MENU */

#menu-and-buttons-wrapper,
.content {
    // color: red;

    background-color: #eee !important;
}
</style>
