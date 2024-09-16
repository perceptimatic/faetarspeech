---
layout: default
---

##### Table of Contents  
[Summary](#summary)\
[Data](#data)\
[Ground Rules](#ground-rules)\
[Timeline](#timeline)\
[Submission Instructions](#submission-instructions)\
[Leaderboard](#leaderboard)\
[Organizers](#organizers)\
[References](#references)

# Summary

# Data
***
Data were extracted from the Faetar collection of the Heritage Language Variation and Change in Toronto (HLVC) corpus \[1\]. The corpus contains 184 recordings of native Faetar speakers collected in Faeto between 1992 and 1994 (the _Homeland_ subset) and 37 recordings of first- and second-generation heritage Faetar speakers collected in Toronto between 2009 and 2010  (the _Heritage_ subset) \[1\]. Some of the recordings were interviews (_Interview_), designed to elicit spontaneous speech, and, in others, participants were asked to describe scenes and objects from a picture book (_Words_). The recordings were saved at a 44.1 kHz sampling rate (in the case of the Homeland recordings, this is the sampling rate of the digitization from analog cassette tapes). Recordings can be noisy, with considerable background noise, back-channels, and interruptions.

The source data set consisted of long-form recordings, of which 68 of the Homeland recordings, and 26 of the Heritage recordings, had been at least partially phonetically transcribed at the utterance level. Some of the transcriptions (mostly those in the Heritage subset) were extracted from ELAN annotation files, which had utterance-level alignments \cite{brugmanAnnotatingMultimediaMultimodal2004}, while the remainder were extracted from Microsoft Word files, by manually mapping numerical values from each of the two fonts used (PalPhon or IPAPhon) to modern UTF-8 encodings, and removing anything that did not look like a transcription (English glosses, identifiers, _etc._). 

For the portion which was transcribed but not aligned, we adapted the JHU Arabic MGB-3 recipe for segmentation and alignment \cite{manoharJHUKaldiSystem2017}, built on Kaldi \cite{poveyKaldiSpeechRecognition2011}. This splits recordings and recording-level transcriptions by i-vector speaker diarization, splits each diarized segment into smaller, overlapping segments, aligns each overlapping segment to the text (allowing for minor changes to the text) with a seed ASR system, and  stitches the overlapping segments back together using string matching. We trained the seed ASR system on the aligned part of the data. To generate our automatic alignments, we used a monophone, speaker-independent Gaussian mixture model-Hidden Markov model (GMM-HMM) system. We found this worked better than triphone or speaker-dependent models, presumably because of the very limited aligned data we had available for training.  We then used PyAnnote 3.0 \cite{Plaquet23,Bredin23} to adjust utterance boundaries according to voice-activity detection and label them with speaker diarization. Because the pipeline is error-prone, we  manually threw out  utterances whose boundaries were clearly misaligned or whose transcriptions were very clearly wrong. On the test set (see below), we made a second, more rigorous, manual pass to correct alignments. 

After obtaining time-alignments for the whole data set, further filtering was performed to remove the interviewer's speech (generally clearly marked), to remove utterances with duration less than 500~ms, and to remove utterances in Italian or English.  While code-switching is common in Faetar speech (and thus, a recognizer should deal with it) removing utterances with substantial parts of Italian or English did not result in a major loss of data.  As such, we take it that the (simpler) problem we propose, which consists of transcribing Faetar with minimal code-switching, is a reasonable approximation to the real problem. For the purposes of ASR research, it will be easier to interpret the results in a more homogeneous corpus. Nevertheless, as Faetar has been in contact with Italian for a long time, and substantially longer than it has been in contact with English (English only appears in the Heritage portion of the corpus), we took a more lenient approach to identifying Italian utterances. To identify English utterances, the presence of a single English word, drawn from a closed list that were clearly not words in Faetar, was sufficient to mark an utterance as English. On the other hand, for Italian, we required that there be three words in a row, again from a closed list.

We split the aligned data into _train_, _dev_, and _test_, ensuring a reasonable balance between male and female speakers, and between Homeland and Heritage subsets, in both \emph{train} and \emph{test}. We do not include the \emph{Words} subset in the \emph{dev} or \emph{test} splits, as we take it that this is too easy an evaluation: many of the utterances consist of individual words, often the same word. Anticipating compatibility with the ML-SUPERB benchmark \cite{shiFindings2023MLSUPERB2023}, we also construct  \emph{1h} and \emph{10min} subsets of \emph{train}. We distribute the remainder of the data, for which we did not have transcriptions, or for which the (long-form) file could not be time-aligned, as an \emph{unlab}elled set, after obtaining VAD and speaker diarization using PyAnnote 3.0. Because we determined that many of the shorter utterances extracted in this way were not speech, we discarded all unlabelled utterances less than 1.5 seconds. Table \ref{tab:hours} shows the distribution of data in the corpus.
***

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  padding:10px 5px;word-break:normal;}
.tg th{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  font-weight:normal;padding:10px 5px;word-break:normal;background-color:lightblue;color:black;}
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

# Ground Rules
We consider unconstrained and constrained baseline systems,
where by “constrained” we mean that the model is not trained on data
sets other than train and unlab, including pre-trained models trained
on other languages. Considering constrained approaches separately
allows us to focus on questions of model architecture, rather than on
pre-training. As far as constrained models go, as discussed in Section
III-B, force-alignment of transcriptions to audio was performed with
Kaldi [27], initially using a monophone, speaker-independent HMM-
GMM model, and then refined at the end using a triphone, speaker-
dependent model; both were composed with a 5-gram, character-
level, modified Kneser-Ney language model [30] trained on the (post 
alignment) transcriptions from the train partition. We report the
performance for these models in Table III, ± the half width of a 95%
bootstrap confidence interval calculated using K = 10000 samples.
Alternatively, we train using the ML-SUPERB recipe [1] from
ESPNet [31] using filterbanks, keeping all hyperparameters as-is
except to set the effective batch size to 4. The model consists of
a single convolutional layer followed by two transformer layers,
trained using CTC. This was substantially better than the HMM-
GMM model.3 Decoding with a 5-gram language model trained on
train did not improve PERs, presumably because the neural model
already exhausted what can be learned from train. For comparison
with ML-SUPERB, we also include results for the restricted 1hr and
10min training conditions.
In the unconstrained condition, we fine-tune existing multilingual
models MMS [32] and mHuBERT [33] on the train set. Both are
masked prediction models; MMS is a wav2vec 2.0 model that takes a
language-specific adapter, head, and fine-tuning strategy. Rather than
initializing the adapter layers from scratch, we initialize the adapters
and head with a model fine-tuned on Italian. mHuBERT takes an
iterative refinement approach, training first on classification according
to classes derived from k-means clustering on spectral features, then,
after the first iteration, on targets derived from clustering the internal
representations of the previous one. As [33] obtained best results with
three iterations, we fine-tune the third iteration. For both models,
we use a linear schedule with peak learning rate of 1e−5 for 200
epochs of which ten are warmup, dropout of 10%, and effective
batch size of 8. Both give substantially better results than ESPnet,
and the differences in performance between the two are minor, with
MMS having a slight advantage (within the overlap of the confidence
intervals).

# Timeline 
challenge results submission deadline - XXXXXXX \
interspeech 2025 paper submission deadline - feb 12
# Submission Instructions
# Leaderboard
add results of baseline models
name   constraints   per

constrained leaderboard
<table id="cLeader">
  <tr>
    <th>Name</th>
    <th onclick="sortTable(1, cLeader)">PER</th>
  </tr>
  <tr>
    <td>HMM-GMM Mono + 5-gram (baseline)</td>
    <td>62.6</td>
  </tr>
  <tr>
    <td>HMM-GMM Tri + 5-gram (baseline)</td>
    <td>56.7</td>
  </tr>
  <tr>
    <td>ESPnet train (baseline)</td>
    <td>35.9</td>
  </tr>
  <tr>
    <td>ESPnet 1hr (baseline)</td>
    <td>37.4</td>
  </tr>
  <tr>
    <td>ESPnet 10min (baseline)</td>
    <td>45.1</td>
  </tr>
</table>

unconstrained leaderboard
<fieldset>
<div>
	<input type="checkbox" id="constrained" name="constrained"/>
	<label for="constrained">Constrained</label>
</div>

<div>
	<input type="checkbox" id="unlab" name="unlab" />
	<label for="unlab">Unlab</label>
</div>

<div>
	<input type="checkbox" id="extra_docs" name="extra_docs" />
	<label for="extra_docs">Extra Docs</label>
</div>
</fieldset>

<table id="Leader">
  <tr>
    <th>Name</th>
    <th onclick="sortTable(1, Leader)">PER</th>
    <th onclick="filter(2, Leader)">Constrained</th>
  </tr>
  <tr>
    <td>HMM-GMM Mono + 5-gram (baseline)</td>
    <td>62.6</td>
  </tr>
  <tr>
    <td>HMM-GMM Tri + 5-gram (baseline)</td>
    <td>56.7</td>
  </tr>
  <tr>
    <td>ESPnet train (baseline)</td>
    <td>35.9</td>
  </tr>
  <tr>
    <td>ESPnet 1hr (baseline)</td>
    <td>37.4</td>
  </tr>
  <tr>
    <td>ESPnet 10min (baseline)</td>
    <td>45.1</td>
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
function filter(n, table_id) {
  var table, tr, td, i, txtValue;
  table = document.getElementById("myTable");
  tr = table.getElementsByTagName("tr");
  for (i = 0; i < tr.length; i++) {
    td = tr[i].getElementsByTagName("td")[0];
    if (td) {
      txtValue = td.textContent || td.innerText;
      if (txtValue.indexOf(filter) > -1) {
        tr[i].style.display = "";
      } else {
        tr[i].style.display = "none";
      }
    }       
  }
}
<body onload = function() {
	(table = document.getElementById("cLeader");
		table.getElementsByTagName("th")[1]).click();
    };>
</script>


vs the rest checkboxes for unlab / extra docs / unconstrained

# Organizers

# References
- \[1\] N. Nagy, “A multilingual corpus to explore variation in language contact
situations,” _RILA_, pp. 65–84, 2011.
