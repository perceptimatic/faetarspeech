---
layout: default
title: The Faetar Low-Resource ASR Challenge
---

- [The Faetar Language](#the-faetar-language)
- [Ground Rules](#ground-rules)
- [Tracks](#tracks)
- [Criteria for Judging Submissions](#criteria-for-judging-submissions)
- [Data and Licensing](#data-and-licensing)
	- [Alternate splits](#alternate-splits)
	- [Dirty Data](#dirty-data)
- [Timeline](#timeline)
- [How to Participate](#how-to-participate)
	- [Dev kit](#dev-kit)
	- [Registering/requesting data access](#registeringrequesting-data-access)
	- [How to submit](#how-to-submit)
- [Leaderboard](#leaderboard)
- [Contact](#contact)
- [Organizers](#organizers)
- [References](#references)


Low-resource speech recognition has gained substantial attention in recent years, particularly with the advent of large multilingual speech foundation models and language models. This is welcome, as there are thousands of languages which have existing small partially transcribed collections of field or found recordings, but no ASR systems. Such technology would be transformative for linguists, educators, and the numerous minoritized communities worldwide who face challenges to the survival of their languages and cultures. This technology would allow for recorded speech to be valorized and made more accessible, for the benefit of current and future speakers of these languages. However, a clear picture of best practices when developing ASR systems in very low-resource contexts has not yet emerged.

The Faetar Low-Resource ASR Challenge aims to focus researchers’ attention on several issues which are common to many archival collections of speech data:

* **noisy** field recordings
* lack of standard orthography, leading to **noise in the transcriptions** in the form of transcriber inconsistencies
* **only a few hours** of transcribed data
* a larger collection of **untranscribed data**
* **no additional data** in the language (textual or speech) that is easily available
* **“dirty” transcriptions** in documents, which contain matter that needs to be filtered out

By focusing multiple research groups on a single corpus of this kind, we aim to gain deeper insights into these problems than can be achieved otherwise.

***The challenge will run from November 1st 2024 to February 1st 2025. We encourage participants to submit papers to Interspeech 2025 (main conference). See [Timeline](#timeline) for detailed timeline.***

## The Faetar Language

**Please see [Ong et al. 2024](https://arxiv.org/abs/2409.08103) for more details about the Faetar ASR Benchmark Corpus.**

The challenge uses the Faetar ASR Benchmark Corpus. Faetar (pronounced [fajdar]) is a variety of the Franco-Provençal language which developed in isolation in Italy, far from other speakers of Franco-Provençal, and in close contact with Italian. Faetar has less than 1000 speakers around the world, in Italy and in the diaspora. It is endangered, and preservation, learning, and documentation are a priority for many community members. The benchmark data represents the majority of all archived speech recordings of Faetar in existence, and it is not available from any other source.

Data were extracted from the Faetar collection of the Heritage Language Variation and Change in Toronto (HLVC) corpus [1]. The corpus contains 184 recordings of native Faetar speakers collected in Italy between 1992 and 1994 (the Homeland subset) and 37 recordings of first- and second-generation heritage Faetar speakers collected in Toronto between 2009 and 2010 (the Heritage subset). All come from field recordings, generally noisy, of semi-spontaneous speech. 

Faetar has no standard written form. The data set is transcribed quasi-phonetically for linguistic purposes in IPA. The transcriptions are not always consistent, as different parts of the data set were transcribed for different purposes: sometimes the transcription is narrow and phonetic, while at other times the transcription is broad and phonemic.


## Ground Rules

- Participants will make use of the training data provided (~4.5 hrs) and will submit phone-level decodings for train, dev and test audio.
- Participants will not have access to the test transcriptions during the period of the challenge and organizers will perform the final evaluation on the test set.
- Participants are provided with a dev kit that allows them to calculate scores on the dev and train sets.
- To ensure that participants can be confident in their results before submission, while maintaining comparability across participants, we also propose standardized alternative splits within the train set, which participants can use to do held-out evaluations without relying only on the small dev set.
- Participants must sign a data agreement preventing redistribution before accessing the data set.
- Each research group may make **no more than four submissions** for evaluation.

## Tracks


- **Constrained ASR.** Participants should focus on the challenge of improving ASR architectures to work with small, poor-quality sets. Participants may not use any  resources to train / fine-tune their models beyond the files contained in the provided training data. No external pre-trained acoustic models or language models are allowed. Use of the unlabelled portion of the Faetar challenge data set is allowed (**unlab**) in addition to **train**, as long as this is indicated in the submission, and as long as no external resources (including pre-trained models) are used.

Three other "thematic tracks" can be explored, and should not be considered mutually exclusive:

-  **Using pre-trained acoustic models or language models.** Participants focus on the most effective way to make use of models pre-trained on other languages.
-  **Using unlabelled data.** The challenge data also includes ~20 hrs of unlabelled data. Participants focus on finding the most effective way to make use of it.
- **Dirty data.** The training data was extracted and automatically aligned from long-form audio and partial transcriptions in “cluttered” word processor files, relying on (error-prone) VAD, scraping, and alignment. Participants focus on improving the pipeline for extracting useful training data, with the ultimate goal of improving performance. *Participants seeking to participate in the Dirty Data challenge should indicate this on the registration form.*

Participants should indicate at the time of submission whether they are making a **Constrained ASR** submission, and, otherwise, which of the three thematic tracks they are submitting to (possibly more than one).

Each research group may make **no more than four submissions total** for evaluation, across all tracks.


## Co-submission to the ML-SUPERB Challenge

Many participants in the Faetar Challenge may also wish to participate in the ML-SUPERB 2.0 2025 Challenge, which has been tentatively accepted as a special session at Interspeech 2025. The ML-SUPERB 2.0 benchmark focuses on developing approaches to ASR which are robust across languages and language varieties. Participants in the Faetar challenge with systems that can also be fruitfully evaluated on the ML-SUPERB 2.0 benchmark are strongly encouraged to submit their papers to the ML-SUPERB session at Interspeech. For example, a submission may attempt to make efficient use of the unlabelled set by using it as additional pre-training data for a multilingual speech foundation model, while also improving the architecture of the underlying model, leading the participants to seek to evaluate the improved model on the ML-SUPERB benchmark; other potential points of contact might include explorations of improving speech enhancement, language model fusion, speaker normalization, or other traditional ASR techniques which might be relevant to the challenges posed by the Faetar corpus.

For more information, see the ML-SUPERB 2.0 website at: [https://multilingual.superbbenchmark.org/](https://multilingual.superbbenchmark.org/)


## Criteria for Judging Submissions

Submissions will be evaluated on phone error rate (PER) on the test set. Participants are provided with a [dev kit](#dev-kit) allowing them to calculate the PER on dev and train, as well as reproduce the baselines. Bootstrap confidence intervals can also be calculated using the dev kit to demonstrate robustness.

A winner or tie will be declared based on PER and confidence intervals. All submissions falling within a 95% confidence interval of the submission with the lowest PER will be considered to have won, with the submission having the numerically lowest PER being awarded a special distinction.

(An) **overall winner(s)** will be declared, as well as (a) winner(s) of the **Constrained ASR** track. The results of the challenge will also indicate the best approaches within the three other subtracks.


## Data and Licensing

**Please see [Ong et al. 2024](https://arxiv.org/abs/2409.08103) for more details about the Faetar ASR Benchmark Corpus and a more detailed breakdown of the corpus.**

The Faetar ASR Benchmark Corpus data used in the challenge is available without cost **under a restrictive license that prohibits re-distribution, among other things.** Please see the **Registration** section below to request access.

The following table shows the distribution of data in the corpus, which consists of a **train** set, a **test** set, a small **dev** set, and an **unlab**elled set. 

<table><thead>
  <tr>
    <th>Split</th>
    <th>Usage in the challenge</th>
    <th>Amount</th>
  </tr></thead>
<tbody>
  <tr>
    <td>train</td>
    <td><em>Training set (all tracks); <strong>Constrained ASR</strong> track: no data beyond this set can be used for training</em></td>
    <td>4:30:17</td>
  </tr>
  <tr>
    <td>dev</td>
    <td><em>Validation; held-out evaluation before submission to the challenge</em></td>
    <td>11:49</td>
  </tr>
  <tr>
    <td>unlab</td>
    <td><em>Additional resource in <strong>Unlabelled data</strong> track.</em></td>
    <td>19:55:21</td>
  </tr>
  <tr>
    <td>test</td>
    <td><em>Final evaluation: transcripts are unavailable to participants</em></td>
    <td>46:54</td>
  </tr>
</tbody></table>


#### Alternate splits


Since the **test** set is unavailable to challenge participants during the duration of the challenge, we recommend that participants not rely entirely on **dev** for held-out evaluation. In order to increase the amount of data available for held-out evaluation, we have created an alternate split of the **train** set compraised of the sets **1h** and **reduced_train** (train minus 1h), so that the set **1h** can be used as a held-out evaluation set.
We will also provide benchmark results (*to come*) for the alternative subsets within **train**.
The following table shows the distribution of the alternative splits:

<table>
<thead>
  <tr>
    <th>Split</th>
    <th>Suggested usage</th>
    <th>Amount</th>
  </tr>
</thead>
<tbody>
<tr>
    <td>1h</td>
    <td><em>Hold out to use as additional validation/development data; <strong>or</strong> use as alternate train set to evaluate lower-data circumstances</em></td>
    <td>58:34</td>
</tr>
<tr>
    <td>reduced_train (i.e. train minus 1h)</td>
    <td><em>Use as alternate train set when evaluating on the above alternate split(s)</em></td>
    <td>3:40:32</td>
</tr>
</tbody>
</table>

#### Dirty data

The benchmark corpus was extracted and automatically aligned from long-form audio and (incomplete) transcriptions that were scraped from word processor files that often contained other, irrelevant material, then aligned to the utterance level (see [Ong et al. 2024](https://arxiv.org/abs/2409.08103) for more details). Participants in the **Dirty data** track will seek to improve on the process (scraping, segmenting, aligning), with the goal of **improving the quality of the train set**. The ultimate goal remains the same, of improving PER on the test set.

The **dirty data** collection consists of the original source files (audio and transcriptions) for a subset of **train** that does not overlap with **test** or **dev** (In the standard benchmark corpus, some of the full audio files were split by speaker between train and dev/test), some of the mapping files that we used during the first stages of extraction and filtration of the data, and a summary of the process that was used to extract the data. Please request the dirty data set on the registration form if you intend to use it.

For participants using the dirty data, we have also created a reference subset **dirty_data_train** of **train** which only contains utterances taken from the **dirty data** files. Baseline results will be provided for this subset for reference. The improved training sets that participants will create from the dirty data are  expected to be different from **dirty_data_train**.

## Timeline 

- **November 1st, 2024:** Release of data, opening of challenge
- **February 1st, 2025:** Participants must submit system description(s) and test decodings
- **February 5th, 2025:** Participants receive test scores from organizers, winners announced
- **February 12th, 2025:** Interspeech paper submission deadline
- **February 19th, 2025:** Interspeech paper update deadline
- **May 21st, 2025:** Interspeech paper acceptance notification
- **August 17-25, 2025:** Interspeech conference

## How to Participate

#### Dev kit

Please access the dev kit, permitting you to evaluate your system and replicate baselines here (does not include the data) at [https://github.com/perceptimatic/faetar-dev-kit](https://github.com/perceptimatic/faetar-dev-kit).

#### Registering/requesting data access

*Requests for access to the data will be responded to within 24 hrs. You will receive a download link if your request is approved.*

<iframe width="640px" height="480px"
    src="https://forms.office.com/r/qanCB2sjbM?embed=true" frameborder="0"
    marginwidth="0" marginheight="0"
    style="border: none; max-width:100%; max-height:100vh" allowfullscreen
    webkitallowfullscreen mozallowfullscreen msallowfullscreen> </iframe>

#### How to submit

Each research group may make **no more than four submissions** for evaluation.

The filenames of the test decoding submissions should contain the name of the team, the name of the model used, and be in the following format:

the quick brown fox jumps over the lazy dog (utterance_a)
pack my box with five dozen liquor jugs (utterance b)
...(etc.)

*Details of submission process to be announced*

## Leaderboard

At the outset of the challenge, this will contain only the baseline model results.  **Please see [Ong et al. 2024](https://arxiv.org/abs/2409.08103) for details about the baseline models.**

<fieldset>

<div>
	<input type="checkbox" id="constrained" name="constrained"
        onclick="drop_box_filter('Leader')"/>
	<label for="constrained">Constrained</label>
</div>

<div>
	<input type="checkbox" id="extr" name="extr"
        onclick="drop_box_filter('Leader')"/>
	<label for="extr">External pre-trained AM/LM</label>
</div>


<div>
	<input type="checkbox" id="unlab" name="unlab"
        onclick="drop_box_filter('Leader')"/>
	<label for="unlab">Uses unlab</label>
</div>


<div>
	<input type="checkbox" id="dirty" name="dirty"
        onclick="drop_box_filter('Leader')"/>
	<label for="dirty">Dirty data challenge</label>
</div>

</fieldset>

<table id="Leader">
  <tr>
    <th>Research group</th>
		<th>Description</th>
		<th>Training set</th>
        <th>Constrained</th>
		<th>External pre-trained AM/LM</th>
		<th>Uses unlab</th>
		<th>Dirty data challenge</th>
    <th onclick="sortTable(7, 'Leader')">PER on test</th>
  </tr>
  <tr>
		<td>Organizers (baseline)</td> 
    <td>Kaldi HMM-GMM Mono + 5-gram Kneser-Ney [6,7]</td>
    <td>train</td>
    <td>x</td>
		<td></td>
		<td></td>
		<td></td>
    <td>62.6</td>
  </tr>
  <tr>
		<td>Organizers (baseline)</td> 
    <td>Kaldi HMM-GMM Tri + 5-gram Kneser-Ney [6,7]</td>
    <td>train</td>
		<td>x</td>
		<td></td>
		<td></td>
		<td></td>
    <td>56.7</td>
  </tr>
  <tr>
		<td>Organizers (baseline)</td> 
    <td>ESPnet ML-SUPERB [2,3]</td>
    <td>train</td>
		<td>x</td>
		<td></td>
		<td></td>
		<td></td>
    <td>35.8</td>
  </tr>
  <tr>
		<td>Organizers (baseline)</td> 
    <td>ESPnet ML-SUPERB [2,3]</td>
    <td>1hr</td>
		<td>x</td>
		<td></td>
		<td></td>
		<td></td>
    <td>37.4</td>
  </tr>
  <tr>
		<td>Organizers (baseline)</td> 
    <td>ESPnet ML-SUPERB [2,3]</td>
    <td>10m</td>
		<td>x</td>
		<td></td>
		<td></td>
		<td></td>
    <td>45.1</td>
  </tr>
  <tr>
		<td>Organizers (baseline)</td> 
    <td>MMS [4]</td>
		<td>train</td>
		<td></td>
		<td>x</td>
		<td></td>
		<td></td>
    <td>33.0</td>
  </tr>
	<tr>
		<td>Organizers (baseline)</td> 
    <td>mHubert-147 [5]</td>
		<td>train</td>
		<td></td>
		<td>x</td>
		<td></td>
		<td></td>
    <td>33.6</td>
  </tr>
	<tr>
		<td>Organizers (baseline)</td> 
    <td>MMS [4] continued pre-training</td>
		<td>train</td>
		<td></td>
		<td>x</td>
		<td>x</td>
		<td></td>
    <td>31.5</td>
  </tr>
	<tr>
		<td>Organizers (baseline)</td> 
    <td>MMS [4] self-training</td>
		<td>train</td>
		<td></td>
		<td>x</td>
		<td>x</td>
		<td></td>
        <td>31.0</td>
  </tr>
	<tr>
		<td>Organizers (baseline)</td> 
    <td>MMS [4] pre-training + self-training</td>
		<td>train</td>
		<td></td>
		<td>x</td>
		<td>x</td>
		<td></td>
        <td>30.4</td>
  </tr>
</table>

<script>

function sortTable(n, table_id) {
  var table, rows, switching, i, x, y, shouldSwitch;
  table = document.getElementById(table_id);
  switching = true;
  /* Make a loop that will continue until
  no switching has been done: */
  while (switching) {
    // Start by saying: no switching is done:
    switching = false;
    rows = table.rows;
    /* Loop through all table rows (except the
    first, which contains table headers): */
    for (i = 1; i < (rows.length - 1); i++) {
      // Start by saying there should be no switching:
      shouldSwitch = false;
      /* Get the two elements you want to compare,
      one from current row and one from the next: */
      x = rows[i].getElementsByTagName("td")[n];
      y = rows[i + 1].getElementsByTagName("td")[n];
      if (Number(x.innerHTML) > Number(y.innerHTML)) {
        // If so, mark as a switch and break the loop:
        shouldSwitch = true;
        break;
      }
    }
    if (shouldSwitch) {
      /* If a switch has been marked, make the switch
      and mark that a switch has been done: */
      rows[i].parentNode.insertBefore(rows[i + 1], rows[i]);
      switching = true;
    }
  }
}

function drop_box_filter(table_id) {

    let cb_const = document.getElementById('constrained').checked;    
    let cb_extr = document.getElementById('extr').checked; 
    let cb_unlab = document.getElementById('unlab').checked; 
    let cb_dirty = document.getElementById('dirty').checked; 
    
    var table = document.getElementById(table_id);
        
    for (var i = 1, row; row = table.rows[i]; i++) {
    	if ((cb_const && row.cells[3].innerText !== 'x')
            || (cb_extr && row.cells[4].innerText !== 'x')
            || (cb_unlab && row.cells[5].innerText !== 'x')
            || (cb_dirty && row.cells[6].innerText !== 'x')
            ) {
            row.style = "display:none";
        }
        else {
            row.style = "display:table-row";
        }
    }     

}
function run_sort(table_id) {
    table = document.getElementById(table_id);
    table.getElementsByTagName("th")[7].click();
}

window.onload = run_sort('Leader');

</script>

## Contact

Questions should be directed to <em>faetarasrchallenge at gmail dot com</em>.

## Organizers

- Ewan Dunbar, University of Toronto
- Michael Ong, University of Toronto
- Leo Peckham, University of Toronto
- Naomi Nagy, University of Toronto

## References

<a id="1">[1]</a> N. Nagy, "A multilingual corpus to explore variation in language contact situations," _RILA_, pp. 65–84, 2011.

<a id="2">[2]</a> S. Watanabe, T. Hori, S. Karita, T. Hayashi, J. Nishitoba, Y. Unno, N. Enrique Yalta Soplin, J. Heymann, M. Wiesner, N. Chen, A. Renduchintala, and T. Ochiai, “ESPnet: End-to-end speech processing toolkit,” in Proc. Interspeech 2018, 2018, pp. 2207–2211.

<a id="3">[3]</a> J. Shi, W. Chen, D. Berrebbi, H.-H. Wang, W.-P. Huang, E.-P. Hu, H.-L. Chuang, X. Chang, Y. Tang, S.-W. Li, A. Mohamed, H.-Y. Lee, and S. Watanabe, “Findings of the 2023 ML-SUPERB challenge: Pretraining and evaluation over more languages and beyond,” in ASRU, 2023, pp. 1–8.

<a id="4">[4]</a> V. Pratap, A. Tjandra, B. Shi, P. Tomasello, A. Babu, S. Kundu, A. Elkahky, Z. Ni, A. Vyas, M. Fazel-Zarandi, A. Baevski, Y. Adi, X. Zhang, W.-N. Hsu, A. Conneau, and M. Auli, “Scaling speech technology to 1,000+ languages,” 2023.

<a id="5">[5]</a> M. Z. Boito, V. Iyer, N. Lagos, L. Besacier, and I. Calapodescu, “mhubert-147: A compact multilingual hubert model,” arXiv preprint arXiv:2406.06371, 2024.

<a id="6">[6]</a>  D. Povey, A. Ghoshal, G. Boulianne, L. Burget, O. Glembek, N. Goel, M. Hannemann, P. Motlicek, Y. Qian, P. Schwarz, J. Silovsky, G. Stemmer, and K. Vesely, “The Kaldi speech recognition toolkit,” in ASRU. Hilton Waikoloa Village, Big Island, Hawaii, US: IEEE Signal Processing Society, 2011.

<a id="7">[7]</a>  M. Ong, S. Robertson, L. Peckham, A. J. J. de Aberasturi, P. Arkhangorodsky, R. Huo, A. Sakhardande, M. Hallap, N. Nagy, and E. Dunbar, “The faetar benchmark: Speech recognition in a very under-resourced language,” arXiv preprint arXiv:2409.08103, 2024.

