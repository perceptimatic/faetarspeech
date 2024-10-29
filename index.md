---
layout: default
title: The Faetar ASR Challenge: Speech Recognition in a Very Under-Resourced Language
---

<!--
##### Table of Contents  
- [Challenge Summary](#challenge-summary)
- [Ground Rules](#ground-rules)
- [Data](#data)
- [Timeline](#timeline)
- [Submission Instructions](#submission-instructions)
- [Leaderboards](#leaderboards)
	- [Constrained Models](#constrained-models)
	- [All Models](#all-models)
- [Registration](#registration)
- [Organizers](#organizers)
- [References](#references)
-->

### Challenge Summary

Low-resource speech recognition has gained substantial attention in recent years, particularly with the advent of large multilingual speech foundation models and language models. This is welcome, as there are thousands of languages for which no ASR exists, and, for many of them, small collections of field or found recordings, often partially transcribed, do exist. Such technology would be transformative for linguists, educators, and  for many of the minoritized communities worldwide facing challenges to the survival of their language and culture, allowing them to valorize and make more accessible recorded speech, for the benefit of current and future speakers of the language. However, a clear picture of best practices when developing ASR systems in very low-resource contexts has not yet emerged.

The Faetar ASR Challenge aims to focus researchers’ attention on several issues which are common to many archival collections of speech data:

* **noisy** field recordings
* **only a few hours** of transcribed data
* a larger collection of **untranscribed data**
* **no additional data** in the language (textual or speech) that's easily available
* **“dirty” transcriptions** in documents containing matter that needs to be filtered out

By focusing multiple research groups on a single corpus of this kind, we aim to gain deeper insights into these problems than can be achieved otherwise.

### The Faetar language

**Please see [Ong et al. 2024](https://arxiv.org/abs/2409.08103) for more details about the Faetar ASR Benchmark Corpus.**

The challenge uses the Faetar ASR Benchmark Corpus. Faetar (pronounced [fajdar]) is a variety of the Franco-Provençal language which developed in isolation in Italy, far from other speakers of Franco-Provençal, and in close contact with Italian. Faetar has less than 1000 speakers around the world, in Italy and in the diaspora. It is endangered, and preservation, learning, and documentation are a priority for many community members. The benchmark data represents the majority of all archived speech recordings of Faetar in existence, and it is not available from any other source.

Faetar has no standard written form. The data set is transcribed quasi-phonetically for linguistic purposes in IPA. The transcriptions are not always consistent, as different parts of the data set were transcribed for different purposes: sometimes the transcription is narrow and phonetic, while at other times the transcription is broad and phonemic.

Data were extracted from the Faetar collection of the Heritage Language Variation and Change in Toronto (HLVC) corpus [1]. The corpus contains 184 recordings of native Faetar speakers collected in Italy between 1992 and 1994 (the Homeland subset) and 37 recordings of first- and second-generation heritage Faetar speakers collected in Toronto between 2009 and 2010 (the Heritage subset). All come from field recordings, generally noisy, of semi-spontaneous speech. 


### Ground Rules

- Participants will make use of the training data provided (~4.5 hrs) and will submit phone-level decodings for train, dev and test audio.
- Participants will not have access to the test transcriptions during the period of the challenge and organizers will perform the final evaluation on the test set.
- Participants are provided with a dev kit that allows them to calculate scores on the dev and train sets.
- To ensure that participants can be confident in their results before submission, while maintaining comparability across participants, we also propose standardized alternative splits within the train set, which participants can use to do held-out evaluations without relying only on the small dev set.
- Participants must sign a data agreement preventing redistribution before accessing the data set.

### Tracks

Participants in the **Constrained ASR track** may not use any external resources beyond the training data, including pre-trained acoustic models, language models, or the unlabelled portion of the Faetar challenge data set.


- **Using pre-trained acoustic models or language models.** Participants focus on the most effective way to make use of models pre-trained on other languages.
- **Using unlabelled data.** The challenge data also includes ~20 hrs of unlabelled data. Participants focus on finding the most effective way to make use of it.
- **Dirty data.** The training data was extracted and automatically aligned from long-form audio and partial transcriptions in “cluttered” word processor files, relying on (error-prone) VAD, scraping, and alignment. Participants focus on improving the pipeline for extracting useful training data, with the ultimate goal of improving performance.


###  Criteria for judging submissions

Submissions will be evaluated on phone error rate (PER) on the test set. Participants are provided with a dev kit allowing them to calculate the PER on dev and train, as well as reproduce the baselines. Bootstrap confidence intervals can also be calculated using the dev kit to demonstrate robustness. All submissions falling within a 95% confidence interval of the submission with the highest score will be considered to have won. The submission with the highest score will be awarded a special “best of the best” status.


### Data and licensing

**Please see [Ong et al. 2024](https://arxiv.org/abs/2409.08103) for more details about the Faetar ASR Benchmark Corpus.**

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

**Table 1.** Distribution of data in (hh:)mm:ss.
<table class="tg"><thead>
  <tr>
    <th colspan="2" rowspan="2"></th>
    <th colspan="2">Homeland</th>
    <th colspan="2">Heritage</th>
    <th rowspan="2">Total</th>
  </tr>
  <tr>
    <th>M</th>
    <th>F</th>
    <th>M</th>
    <th>F</th>
  </tr></thead>
<tbody>
  <tr>
    <td>dev</td>
    <td>Int.</td>
    <td>8:43</td>
    <td>0:31</td>
    <td>0:00</td>
    <td>2:35</td>
    <td>11:49</td>
  </tr>
  <tr>
    <td>test</td>
    <td>Int.</td>
    <td>13:10</td>
    <td>13:33</td>
    <td>10:54</td>
    <td>9:16</td>
    <td>46:54</td>
  </tr>
  <tr>
    <td rowspan="2">train</td>
    <td>Words</td>
    <td>42:31</td>
    <td>58:29</td>
    <td>51:44</td>
    <td>9:07</td>
    <td rowspan="2">4:30:17</td>
  </tr>
  <tr>
    <td>Int.</td>
    <td>15:58</td>
    <td>27:56</td>
    <td>32:49</td>
    <td>14:41</td>
  </tr>
  <tr>
    <td>1h</td>
    <td>Int.</td>
    <td>11:08</td>
    <td>13:44</td>
    <td>32:50</td>
    <td>0:51</td>
    <td>58:34</td>
  </tr>
  <tr>
    <td>10min</td>
    <td>Int.</td>
    <td>0:00</td>
    <td>4:25</td>
    <td>5:00</td>
    <td>0:24</td>
    <td>9:49</td>
  </tr>
  <tr>
    <td rowspan="3">unlab</td>
    <td>Words</td>
    <td colspan="2">7:29:11</td>
    <td colspan="2">0:05:24</td>
    <td rowspan="3">19:55:21</td>
  </tr>
  <tr>
    <td>Int.</td>
    <td colspan="2">8:23:18</td>
    <td colspan="2">0:51:31</td>
  </tr>
  <tr>
    <td>Mixed</td>
    <td colspan="2">2:12:47</td>
    <td colspan="2">0:53:09</td>
  </tr>
</tbody></table>

Additionally, the challenge data comes with a set of alternative splits within 


### Baselines

## Baselines

**FIXME**

Baseline models (code included in the dev kit) obtain a best PER of 30.4% on test. A number of other baselines are available, including:

**Constrained:**

ESPnet (model used in ML-SUPERB [5]):	35.8% (±0.8 - limits of 95% bootstrap CI)

**Pre-trained models:**

MMS [6]:					33.0% (±0.8)

mHubert-147 [14]:				33.6% (±0.8)

**Use of unlabelled data:**

MMS Continued pre-training 			31.5% (±0.8)


    MMS Self-training 				31.0% (±0.8)


    MMS Both (Cont. PT+ST)			30.4% (±0.8)

More details can be found in the paper describing the benchmark corpus, Ong et al (2024), “The Faetar Benchmark: Speech Recognition in a Very Under-Resourced Language” ([https://arxiv.org/abs/2409.08103](https://arxiv.org/abs/2409.08103)).

### Timeline 
**FIXME**

October 31, 2024: Release of data, opening of challenge
February 1st, 2025: Participants must submit system description(s) and test decodings
February 5th, 2025: Participants receive test scores from organizers, winners announced


February 12th, 2025: Interspeech paper submission deadline
February 19th, 2025: Interspeech paper update deadline
May 21st, 2025: Interspeech paper acceptance notification
August 17-25, 2025: Interspeech conference



A rough proposed timeline is as follows:

* October 14, 2024 - Submission of challenge proposal to Interspeech

* Late October 2024 - Pre-release of challenge data with hidden test
  transcriptions

* November 18th 2024 - Acceptance/rejection of challenge session at Interspeech
  (if rejected, we encourage participants to submit to the regular Interspeech
  sessions)

* End of January/beginning of February 2025 - participants should submit their
  results for evaluation on test

* February 12th, 2025 - Interspeech paper deadline
    
* August 17-25, 2025 - Interspeech conference

### Submission Instructions
**FIXME**

### Leaderboards
**FIXME**

#### Constrained Models

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

### Registration

**FIXME**

<iframe width="640px" height="480px"
    src="https://forms.office.com/r/qanCB2sjbM?embed=true" frameborder="0"
    marginwidth="0" marginheight="0"
    style="border: none; max-width:100%; max-height:100vh" allowfullscreen
    webkitallowfullscreen mozallowfullscreen msallowfullscreen> </iframe>


### Organizers
**FIXME**

### References

<a id="1">[1]</a> N. Nagy, "A multilingual corpus to explore variation in
language contact situations," _RILA_, pp. 65–84, 2011.

