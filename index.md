---
layout: default
title: The Faetar ASR Challenge: Speech Recognition in a Very Under-Resourced Language
---

##### Table of Contents  
- [Challenge Summary](#challenge-summary)
- [Data](#data)
- [Ground Rules](#ground-rules)
- [Timeline](#timeline)
- [Submission Instructions](#submission-instructions)
- [Leaderboards](#leaderboards)
	- [Constrained Models](#constrained-models)
	- [All Models](#all-models)
- [Registration](#registration)
- [Organizers](#organizers)
- [References](#references)

### Challenge Summary

The main goal of this challenge is to determine the effect of ASR architecture
on the recognition of speech in real-world (i.e. noisy) conditions. We provide
transcriptions and audio (the benchmark) from a single corpus extracted from
field work done on the endangered Franco-Provençal language Faetar. Faetar has
very limited, low-quality data.

We anticipate the challenge to run from November 2024 to February 2025 (3
months), culminating in a (proposed) special session at Interspeech 2025.

### Motivation

Although we already have lots of breadth in the evaluation of ASR across
languages (e.g., ML-SUPERB), we need more depth. A challenge task will allow
participants to pay close attention to a single problem, and we are hoping this
will allow us to more fully understand some of the techniques, both old and
new, that participants apply.

The benchmark data is relatively small, is in a language with (almost) no other
sources of data, and is a single language corpus. We posit, due to these
factors, that any differences in performance between different ASR systems in
this challenge are due to differences in their architecture, and the insights
gained through this work will be generalizable to other endangered languages
with low quality recordings.

Another goal of this challenge is to create ASR systems capable of transcribing
Faetar recordings in order to help preserve the language for future
generations. We believe that posing this challenge to the community will help
speed both the development of ASR for Faetar and the discovery of new insights
into ASR architecture.

### Data

{% include important.html content="
During the challenge, the reference transcriptions for the test set will only
be available to the organizers. Following the challenge, the entire benchmark
will be released. See below for registration.
" %}

Data were extracted from the Faetar collection of the Heritage Language
Variation and Change in Toronto (HLVC) corpus. The corpus contains 184
recordings of native Faetar speakers collected in Faeto between 1992 and 1994
(the _Homeland_ subset) and 37 recordings of first- and second-generation
heritage Faetar speakers collected in Toronto between 2009 and 2010 (the
_Heritage_ subset) [[1]](#1).

A portion of the recordings had been at least partially phonetically
transcribed at the utterance level. Some of the transcriptions had
utterance-level alignments, while the remainder were extracted from Microsoft
Word files, automatically segmented and aligned. We then automatically adjusted
utterance boundaries according to voice-activity detection and labeled them
with speaker diarization. Because the pipeline is error-prone, we  manually
threw out utterances whose boundaries were clearly misaligned or whose
transcriptions were very clearly wrong. On the test set, we made a second, more
rigorous, manual pass to correct alignments. 

After obtaining time-alignments for the whole data set, further filtering was
performed to remove the interviewer's speech (generally clearly marked), to
remove utterances with duration less than 500ms, and to remove utterances in
Italian or English.

#### Splits

We split the aligned data into _train_, _dev_, and _test_, ensuring a
reasonable balance between male and female speakers, and between Homeland and
Heritage subsets. We distribute the remainder of the data, for which we did not
have transcriptions, or for which the (long-form) file could not be
time-aligned, as an unlabelled set (_unlab_), after obtaining VAD and speaker
diarization. Table 1 shows the distribution of data in the
corpus.


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

### Ground Rules

<!-- TODO -->


We are envisioning four suggested themes for participants to explore:

* **Constrained**: no use of pre-trained acoustic models or any external
  resources, no use of the unlabelled data set - the goal is to concentrate on
  tweaking ASR architectures so that they work better under the difficult
  circumstances presented by this corpus

* **Unconstrained**: pre-trained acoustic models and language models are
  allowed; while participants are very unlikely to find useful resources in the
  language itself, questions about how best to use related languages, or
  benefit from multi-lingual training, in low-resource settings, represent an
  unresolved, current theme in the literature

* **Unlabelled data**: the benchmark contains around 20 hours of unlabelled
  speech data - while this is additional data, it represents a small fraction
  of the amount of data typically used to pre-train speech foundation models;
  how do we best make use of this additional data?

* **Dirty data**: the transcribed part of the corpus was constructed primarily
  from long-form audio files with paired transcripts in Microsoft Word, using
  an imperfect cleaning and alignment pipeline. This is a very common scenario.
  We will make available an additional set of "dirty" data, consisting of the
  source files for the train and unlabelled partitions. Participants can
  experiment with improving upon these data sets using their own pipelines.

### Timeline 

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

### Leaderboards

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

<iframe width="640px" height="480px"
    src="https://forms.office.com/r/qanCB2sjbM?embed=true" frameborder="0"
    marginwidth="0" marginheight="0"
    style="border: none; max-width:100%; max-height:100vh" allowfullscreen
    webkitallowfullscreen mozallowfullscreen msallowfullscreen> </iframe>

<!-- Missing HLVC funding attribution -->

### Organizers

### References

<a id="1">[1]</a> N. Nagy, "A multilingual corpus to explore variation in
language contact situations," _RILA_, pp. 65–84, 2011.

