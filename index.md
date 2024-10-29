---
layout: default
title: The Faetar Low-Resource ASR Challenge
---

- [The Faetar Language](#the-faetar-language)
- [Ground Rules](#ground-rules)
- [Tracks](#tracks)
- [Criteria for Judging Submissions](#criteria-for-judging-submissions)
- [Data and Licensing](#data-and-licensing)
- [Timeline](#timeline)
- [Submission Instructions](#submission-instructions)
- [Leaderboards](#leaderboards)
- [How to Participate](#how-to-participate)
- [Contact](#contact)
- [Organizers](#organizers)
- [References](#references)


Low-resource speech recognition has gained substantial attention in recent years, particularly with the advent of large multilingual speech foundation models and language models. This is welcome, as there are thousands of languages for which no ASR exists, and, for many of them, small collections of field or found recordings, often partially transcribed, do exist. Such technology would be transformative for linguists, educators, and  for many of the minoritized communities worldwide facing challenges to the survival of their language and culture, allowing them to valorize and make more accessible recorded speech, for the benefit of current and future speakers of the language. However, a clear picture of best practices when developing ASR systems in very low-resource contexts has not yet emerged.

The Faetar Low-Resource ASR Challenge aims to focus researchers’ attention on several issues which are common to many archival collections of speech data:

* **noisy** field recordings
* lack of standard orthography leading **noise in the transcriptions** in the form of transcriber inconsistencies
* **only a few hours** of transcribed data
* a larger collection of **untranscribed data**
* **no additional data** in the language (textual or speech) that's easily available
* **“dirty” transcriptions** in documents containing matter that needs to be filtered out

By focusing multiple research groups on a single corpus of this kind, we aim to gain deeper insights into these problems than can be achieved otherwise.

### The Faetar language

**Please see [Ong et al. 2024](https://arxiv.org/abs/2409.08103) for more details about the Faetar ASR Benchmark Corpus.**

The challenge uses the Faetar ASR Benchmark Corpus. Faetar (pronounced [fajdar]) is a variety of the Franco-Provençal language which developed in isolation in Italy, far from other speakers of Franco-Provençal, and in close contact with Italian. Faetar has less than 1000 speakers around the world, in Italy and in the diaspora. It is endangered, and preservation, learning, and documentation are a priority for many community members. The benchmark data represents the majority of all archived speech recordings of Faetar in existence, and it is not available from any other source.

Data were extracted from the Faetar collection of the Heritage Language Variation and Change in Toronto (HLVC) corpus [1]. The corpus contains 184 recordings of native Faetar speakers collected in Italy between 1992 and 1994 (the Homeland subset) and 37 recordings of first- and second-generation heritage Faetar speakers collected in Toronto between 2009 and 2010 (the Heritage subset). All come from field recordings, generally noisy, of semi-spontaneous speech. 

Faetar has no standard written form. The data set is transcribed quasi-phonetically for linguistic purposes in IPA. The transcriptions are not always consistent, as different parts of the data set were transcribed for different purposes: sometimes the transcription is narrow and phonetic, while at other times the transcription is broad and phonemic.




### Ground Rules

- Participants will make use of the training data provided (~4.5 hrs) and will submit phone-level decodings for train, dev and test audio.
- Participants will not have access to the test transcriptions during the period of the challenge and organizers will perform the final evaluation on the test set.
- Participants are provided with a dev kit that allows them to calculate scores on the dev and train sets.
- To ensure that participants can be confident in their results before submission, while maintaining comparability across participants, we also propose standardized alternative splits within the train set, which participants can use to do held-out evaluations without relying only on the small dev set.
- Participants must sign a data agreement preventing redistribution before accessing the data set.
- Each research group may make **no more than four submissions** for evaluation.

### Tracks


1. **Constrained ASR.** Participants should focus on the challenge of improving ASR architectures to work with small, poor-quality sets. May not use any external resources beyond the **train** set. No external pre-trained acoustic models or language models are allowed. The unlabelled portion of the Faetar challenge data set is not allowed either.

Three other "thematic tracks" can be explored, and should not be considered mutually exclusive:

2. **Using pre-trained acoustic models or language models.** Participants focus on the most effective way to make use of models pre-trained on other languages.
3. **Using unlabelled data.** The challenge data also includes ~20 hrs of unlabelled data. Participants focus on finding the most effective way to make use of it.
4. **Dirty data.** The training data was extracted and automatically aligned from long-form audio and partial transcriptions in “cluttered” word processor files, relying on (error-prone) VAD, scraping, and alignment. Participants focus on improving the pipeline for extracting useful training data, with the ultimate goal of improving performance. *Participants seeking to participate in the Dirty Data challenge should indicate this on the registration form.*

Participants should indicate at the time of submission whether they are making a **Constrained ASR** submission, and, otherwise, which of the three thematic tracks they are submitting to (possibly more than one).

Each research group may make **no more than four submissions total** for evaluation, across all tracks.


###  Criteria for judging submissions

Submissions will be evaluated on phone error rate (PER) on the test set. Participants are provided with a dev kit allowing them to calculate the PER on dev and train, as well as reproduce the baselines. Bootstrap confidence intervals can also be calculated using the dev kit to demonstrate robustness.

A winner or tie will be declared based on PER and confidence intervals. All submissions falling within a 95% confidence interval of the submission with the lowest PER will be considered to have won, with the submission having the numerically lowest PER being awarded a special distinction.

(An) **overall winner(s)** will be declared, as well as (a) winner(s) of the **Constrained ASR** track. The results of the challenge will also indicate the best approaches within the three other subtracks.


### Data and licensing

**Please see [Ong et al. 2024](https://arxiv.org/abs/2409.08103) for more details about the Faetar ASR Benchmark Corpus and a more detailed breakdown of the corpus.**

The Faetar ASR Benchmark Corpus data used in the challenge is available without cost **under a restrictive license that prohibits re-distribution, among other things.** Please see the **Registration** section below to request access.

Table 1 shows the distribution of data in the corpus, which consists of a **train** set, a **test** set, a small **dev** set, and an **unlab**elled set. 

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  padding:10px 5px;word-break:normal;}
.tg th{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  font-weight:normal;padding:10px 5px;word-break:normal;background-color:lightblue;color:black;cursor:pointer;}
.tg th, .tg td {text-align:center;vertical-align:middle}
</style>

<table class="tg"><thead>
  <tr>
    <th>Split</th>
    <th>Usage in the challenge</th>
    <th>Amount</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>train</td>
    <td><em>Training models (all tracks); <b>Constrained</b> track: no data beyond this set can be used for training</em></td>
    <td>4:30:17</td>
  </tr>
  <tr>
    <td>dev</td>
    <td><em>Validation; held-out evaluation before submission to the challenge</em></td>
    <td>11:49</td>
  </tr>
  <tr>
    <td>unlab</td>
    <td><em>Additional resource in <b>Unlabelled data</b> track.</em></td>
    <td>19:55:21</td>
  </tr>
  <tr>
    <td>test</td>
    <td><em>Final evaluation: not available to participants</em></td>
    <td>46:54</td>
  </tr>
</tbody></table>


#### Alternate splits

Because the **test** set is unavailable to challenge participants during the duration of the challenge, we recommend that participants not rely entirely on **dev** for held-out evaluation. To this end, we will also provide benchmark results (*to come*) based on the following alternative splits within **train** (provided):

<table class="tg">
<thead>
  <tr>
    <th>Split</th>
    <th>Suggested usage</th>
    <th>Amount</th>
  </tr>
</thead>
<tbody>

<tr>
    <th>10 minutes</th>
    <th><em>Hold out to use as additional validation/development data; or use as alternate train set to explore extreme low-data settings</em></th>
    <th>9:49</th>
</tr>
<tr>
    <th>{1 hour} - {10 minutes}</th>
    <th><em>Hold out to use as additional validation/development data; or use as alternate train set to evaluate lower-data circumstances</em></th>
    <th>48:45</th>
</tr>
<tr>
    <th>{train} - {1 hour} - {10 minutes}</th>
    <th><em>Use as alternate train set when evaluating on the above alternate split(s)</em></th>
    <th>3:40:32</th>
</tr>
</tbody>
</table>

#### Dirty data

The benchmark corpus was extracted and automatically aligned from long-form audio and (incomplete) transcriptions that were scraped from word processor files that often contained other, irrelevant material, then aligned to the utterance level (see [Ong et al. 2024](https://arxiv.org/abs/2409.08103) for more details). Participants in the **Dirty data** track will seek to improve on the process (scraping, segmenting, aligning), with the goal of **improving the quality of the train set**.

The **dirty data** collection consists of the original source files for a subset of **train** that does not overlap with **test** or **dev**, along with the scripts that we used for the first stages of extraction. Please request the dirty data set on the registration form if you intend to use it. Baseline results for training on this subset will be provided (*to come*).

### Timeline 

- **October 31, 2024:** Release of data, opening of challenge
- **February 1st, 2025:** Participants must submit system description(s) and test decodings
- **February 5th, 2025:** Participants receive test scores from organizers, winners announced
- **February 12th, 2025:** Interspeech paper submission deadline
- **February 19th, 2025:** Interspeech paper update deadline
- **May 21st, 2025:** Interspeech paper acceptance notification
- **August 17-25, 2025:** Interspeech conference

### How to Participate

#### Dev Kit

Please access the dev kit, permitting you to evaluate your system and replicate baselines here (does not include the data) at [https://github.com/perceptimatic/faetar-dev-kit](https://github.com/perceptimatic/faetar-dev-kit).

#### Registering/requesting data access

*Requests for access to the data will be responded to within 24 hrs. You will receive a download link if your request is approved.*

<iframe width="640px" height="480px"
    src="https://forms.office.com/r/qanCB2sjbM?embed=true" frameborder="0"
    marginwidth="0" marginheight="0"
    style="border: none; max-width:100%; max-height:100vh" allowfullscreen
    webkitallowfullscreen mozallowfullscreen msallowfullscreen> </iframe>

#### How to Submit

*To be announced*

### Leaderboards

#### Constrained Models only

<fieldset>
	<select id="csubmission_names"
        onchange="drop_filter('csubmission_names', 'cLeader')">
  	<option>Submission Names</option>
	</select>
</fieldset>

<table id="cLeader">
  <tr>
    <th>Submission</th>
    <th>Description</th>
    <th onclick="sortTable(2, 'cLeader')">PER</th>
  </tr>
  <tr>
		<td>baseline</td> 
    <td>HMM-GMM Mono + 5-gram</td>
    <td>62.6</td>
  </tr>
  <tr>
		<td>baseline</td> 
    <td>HMM-GMM Tri + 5-gram</td>
    <td>56.7</td>
  </tr>
  <tr>
		<td>baseline</td> 
    <td>ESPnet train</td>
    <td>35.9</td>
  </tr>
  <tr>
		<td>baseline</td> 
    <td>ESPnet 1hr</td>
    <td>37.4</td>
  </tr>
  <tr>
		<td>baseline</td> 
    <td>ESPnet 10min</td>
    <td>45.1</td>
  </tr>
</table>

#### All Models

<fieldset>
<div>
	<select id="all_submission_names"
        onchange="drop_box_filter('all_submission_names', 'Leader')">
  	<option>Submission Names</option>
	</select>
</div>
<div>
	<input type="checkbox" id="constrained" name="constrained"
        onclick="drop_box_filter('all_submission_names', 'Leader')"/>
	<label for="constrained">Constrained</label>
</div>

<div>
	<input type="checkbox" id="unconstrained" name="unconstrained"
        onclick="drop_box_filter('all_submission_names', 'Leader')"/>
	<label for="unconstrained">Unconstrained</label>
</div>

<hr> 

<div>
	<input type="checkbox" id="train_default" name="train_default"
        onclick="drop_box_filter('all_submission_names', 'Leader')"/>
	<label for="train_default">Default Train (no Unlab or Unclean)</label>
</div>

<hr> 

<div>
	<input type="checkbox" id="unlab" name="unlab"
        onclick="drop_box_filter('all_submission_names', 'Leader')"/>
	<label for="unlab">Unlab</label>
</div>

<div>
	<input type="checkbox" id="lab" name="lab"
        onclick="drop_box_filter('all_submission_names', 'Leader')"/>
	<label for="lab">Labelled</label>
</div>

<hr> 

<div>
	<input type="checkbox" id="extra_docs" name="extra_docs"
        onclick="drop_box_filter('all_submission_names', 'Leader')"/>
	<label for="extra_docs">Unclean</label>
</div>

<div>
	<input type="checkbox" id="no_extras" name="no_extras"
        onclick="drop_box_filter('all_submission_names', 'Leader')"/>
	<label for="no_extras">Clean</label>
</div>
</fieldset>

<table id="Leader">
  <tr>
    <th>Submission</th>
		<th>Description</th>
    <th onclick="sortTable(2, 'Leader')">PER</th>
    <th>Constrained</th>
		<th>Unlab</th>
		<th>Unclean</th>
  </tr>
  <tr>
		<td>baseline</td> 
    <td>HMM-GMM Mono + 5-gram</td>
    <td>62.6</td>
    <td>x</td>
		<td></td>
		<td></td>
  </tr>
  <tr>
		<td>baseline</td> 
    <td>HMM-GMM Tri + 5-gram</td>
    <td>56.7</td>
		<td>x</td>
		<td></td>
		<td></td>
  </tr>
  <tr>
		<td>baseline</td> 
    <td>ESPnet train</td>
    <td>35.9</td>
		<td>x</td>
		<td></td>
		<td></td>
  </tr>
  <tr>
		<td>baseline</td> 
    <td>ESPnet 1hr</td>
    <td>37.4</td>
		<td>x</td>
		<td></td>
		<td></td>
  </tr>
  <tr>
		<td>baseline</td> 
    <td>ESPnet 10min</td>
    <td>45.1</td>
		<td>x</td>
		<td></td>
		<td></td>
  </tr>
  <tr>
		<td>baseline</td> 
    <td>MMS FT</td>
    <td>33.0</td>
		<td></td>
		<td></td>
		<td></td>
  </tr>
	<tr>
		<td>baseline</td> 
    <td>mHubert FT</td>
    <td>33.6</td>
		<td></td>
		<td></td>
		<td></td>
  </tr>
	<tr>
		<td>baseline</td> 
    <td>MMS PT + FT</td>
    <td>31.5</td>
		<td></td>
		<td>x</td>
		<td></td>
  </tr>
	<tr>
		<td>baseline</td> 
    <td>MMS ST</td>
    <td>31.0</td>
		<td></td>
		<td>x</td>
		<td></td>
  </tr>
	<tr>
		<td>baseline</td> 
    <td>MMS PT + ST</td>
    <td>30.5</td>
		<td></td>
		<td>x</td>
		<td></td>
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

function drop_box_filter(dropdown_id, table_id) {

    let cb1 = document.getElementById('constrained').checked;    
    let cb2 = document.getElementById('unlab').checked; 
    let cb3 = document.getElementById('extra_docs').checked;
    
    let cb4 = document.getElementById('unconstrained').checked;    
    let cb5 = document.getElementById('lab').checked; 
    let cb6 = document.getElementById('no_extras').checked;
    
    let cb7 = document.getElementById('train_default').checked;
    
   	let selection = document.getElementById(dropdown_id);

    var table = document.getElementById(table_id);
        
    for (var i = 1, row; row = table.rows[i]; i++) {
    	if ((cb1 && row.cells[3].innerText !== 'x')
            || (cb2 && row.cells[4].innerText !== 'x')
            || (cb3 && row.cells[5].innerText !== 'x')
            || (cb4 && row.cells[3].innerText === 'x')
            || (cb5 && row.cells[4].innerText === 'x')
            || (cb6 && row.cells[5].innerText === 'x')
            || (cb7 && (row.cells[4].innerText === 'x'
                        || row.cells[5].innerText === 'x'))) {
            row.style = "display:none";
        }
        else {
            if (selection.options[selection.selectedIndex].value
                    == "Submission Names") {
                row.style = "display:table-row";
            }
            else if (row.cells[0].innerText !==
                    selection.options[selection.selectedIndex].value) {
                row.style = "display:none";
            }
            else {
                row.style = "display:table-row";
            }  
        }
    }     

}

function drop_filter(dropdown_id, table_id) {
    let selection = document.getElementById(dropdown_id);
    var table = document.getElementById(table_id);
    for (var i = 1, row; row = table.rows[i]; i++) {
        if (selection.options[selection.selectedIndex].value
                == "Submission Names") {
            row.style = "display:table-row";
        }
        else {
            if (row.cells[0].innerText !==
                    selection.options[selection.selectedIndex].value) {
                row.style = "display:none";
            }
            else {
                row.style = "display:table-row";
            }   
        }
    }
}

function run_sort(table_id) {
    table = document.getElementById(table_id);
    table.getElementsByTagName("th")[2].click();
}

function get_submissions(dropdown_id, table_id) {
    let select = document.getElementById(dropdown_id);
    var table = document.getElementById(table_id);
    let submission_set = new Set();
    for (var i = 1, row; row = table.rows[i]; i++) {
        submission_name = row.cells[0].innerText;
        submission_set.add(submission_name);

    }
    for (const submission of submission_set) {
        let el = document.createElement("option");
        el.textContent = submission;
        el.value = submission;
        select.appendChild(el)
    }
}

window.onload = run_sort('cLeader');
run_sort('Leader');
get_submissions('csubmission_names', 'cLeader');
get_submissions('all_submission_names', 'Leader');

</script>

### Contact

Questions should be directed to <em>faetarasrchallenge at gmail dot com</em>.

### Organizers
**FIXME**

### References

<a id="1">[1]</a> N. Nagy, "A multilingual corpus to explore variation in
language contact situations," _RILA_, pp. 65–84, 2011.

