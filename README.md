<h1 align="center"> "Let Me Just Interrupt You"</h1>
<h3 align="center"> Estimating Effects of Interuptions in Supreme Court Oral Arguments </h3>  
<br>

<!-- Project Reference -->

This final project is inspired by and extends the analysis presented in
<a href="https://core-prod.cambridgecore.org/core/journals/journal-of-law-and-courts/article/let-me-just-interrupt-you-estimating-gender-effects-in-supreme-court-oral-arguments/4870F0FD3BEF0E00AF46F8D64EDA2289"> “Let Me Just Interrupt You”: Estimating Gender Effects in Supreme Court Oral Arguments </a>, forthcoming in the Journal of Law and Courts by Erica Cai, Ankita Gupta, Katherine A. Keith, Brendan O’Connor, and Douglas Rice.
While the original study focuses on identifying gender-based disparities in interruption patterns during U.S. Supreme Court oral arguments, this project extends their work by investigating whether such interruptions also shift the semantic meaning of advocates’ arguments — exploring potential downstream impacts on the framing and substance of legal discourse.

If you use or cite the original dataset or replication code, please include the following citation as requested by the authors:

```bibtex
@article{cai2024interrupt,
  author    = {Cai, Erica and Gupta, Ankita and Keith, Katherine A. and O'Connor, Brendan and Rice, Douglas},
  title     = {``Let Me Just Interrupt You'': Estimating Gender Effects in Supreme Court Oral Arguments},
  journal   = {Journal of Law and Courts},
  year      = {2024},
  note      = {Forthcoming}
}
```

<!-- Project Overview -->
<h2 id="overview">Overview</h2>

<p>
This repository contains a partial replication and computational extension of the article:
<b>Cai, E., Gupta, A., Keith, K. A., O’Connor, B., & Rice, D. (2024)</b>, 
<i>“Let Me Just Interrupt You”: Estimating Gender Effects in Supreme Court Oral Arguments</i>, 
<em>Journal of Law and Courts</em> (Forthcoming).
</p>

<ul>
  <li>
    <a href="https://www.cambridge.org/core/journals/journal-of-law-and-courts/article/let-me-just-interrupt-you-estimating-gender-effects-in-supreme-court-oral-arguments/4870F0FD3BEF0E00AF46F8D64EDA2289" target="_blank">
      Original Article – Journal of Law and Courts
    </a>
  </li>
</ul>

<p>
The original study examines gender disparities in interruptions during U.S. Supreme Court oral arguments, finding that female advocates are more frequently interrupted than male counterparts, even after accounting for experience and case factors.
</p>

<p>
This project extends that analysis by investigating the <b>rhetorical consequences</b> of interruptions. We assess two primary questions:
(1) Do interruptions alter the semantic content of an advocate’s argument?
(2) Are interruptions directed at female advocates more emotionally negative?
</p>

<p>
Using the ConvoKit Supreme Court Corpus (2010–2019), we apply a combination of <b>GloVe-based semantic embeddings</b> and <b>NRC lexicon-based sentiment analysis</b> to 12,663 advocate speech chunks. Additionally, exploratory <b>LDA topic modeling</b> is conducted to examine whether subject-matter variation explains sentiment differences. All analysis is implemented in R and Python, with structured outputs including visualizations, summary statistics, and regression results.
</p>


## Raw Data

The `raw_data/` provided by the original authors contains source datasets used in this analysis. They could be found with the Github page "https://github.com/kakeith/interruptions-supreme-court". These files originate from the following publicly available and cited resources:

- **The Supreme Court Database**  
  Structured metadata about U.S. Supreme Court cases, including term year, docket information, and justice participation.  
  [http://supremecourtdatabase.org](http://supremecourtdatabase.org)

- **ConvoKit’s Supreme Court Oral Arguments Corpus**  
  A transcript-level dataset capturing speaker turns and interactions during oral arguments. The corpus is sourced from Oyez and formatted for computational analysis.  
  [https://convokit.cornell.edu/documentation/supreme_corpus.html](https://convokit.cornell.edu/documentation/supreme_corpus.html)

- **Rafo et al.’s World Gender Name Dictionary**  
  A cross-cultural name-gender mapping resource used to infer advocate gender based on first names.  
  [https://github.com/OpenGenderTracking/globalnamedata](https://github.com/OpenGenderTracking/globalnamedata)

- **GloVe Word Embeddings (100d)**  
  Pre-trained 100-dimensional GloVe vectors used to compute semantic embeddings of advocate speech.  
  [https://nlp.stanford.edu/data/glove.6B.zip](https://nlp.stanford.edu/data/glove.6B.zip)

---

### Additional Derived Files

- **`justice-ideology.txt`**  
  Contains binary liberal/conservative ideology labels for each Supreme Court justice. Ideology is defined as the average of the justice’s Martin–Quinn scores (Martin & Quinn, 2002), with scores < 0 labeled as "liberal" and > 0 as "conservative". 

- **`backchannel.txt`**  
  A manually curated list of phrasal backchannel cues (e.g., “uh-huh”, “okay”, “I see”), used to exclude passive affirmations from the interruption detection process.

## Directory Structure

- <code>Data</code>: Contains raw and processed datasets, including:
  - <code>df_final.csv</code> — Processed chunk-level dataset with metadata.
  - <code>df_final_with_text.csv</code> — Includes cleaned speech text.
  - <code>glove.6B.100d.txt</code> — Pre-trained word vectors from Stanford NLP.
  - <code>name2gender.json</code> — Name-to-gender dictionary from Rafo et al.

- <code>Script</code>: Contains R and Python analysis scripts:
  - <code>PPOL6801_Final_Project.Rmd</code> — RMarkdown file used to generate figures, tables, and final regression outputs.
  - <code>PPOL6801_Final_Project.html</code> — HTML output for better reading.
  - <code>create_analyze_chunks.py</code> — Segments transcripts into speech chunks between justices and advocates.
  - <code>advocate_gender.py</code> — Assigns gender labels to advocates using external name dictionaries.
  - <code>filter.py</code> — Applies filtering logic to remove cases with missing metadata or emotionally charged topics.

  All Python scripts (except the `.Rmd`) were adapted from the original ConvoKit framework and customized to support the specific structure and scope of this replication project.


- <code>Plot</code>: Stores output visualizations used in the paper, such as:
  - <code>Cosine_Similarity.png</code>, <code>Neg_Ratio.png</code>, <code>Top_Words.png</code>, etc.

- <code>Doc</code>: Contains project deliverables:
  - <code>PPOL6801_Final_Project_Report</code> — Final written report.
  - <code>PPOL6801_Final_Project_Slides.pptx</code> — Slide deck for presentation.


<p>All analyses were conducted in R and Python. Data cleaning, modeling, and figure generation can be reproduced from the files above.</p>


<!-- PREREQUISITES -->
<h2 id="prerequisites">Prerequisites</h2>

This project is written in the R programming language and requires the following packages:<br>
`tidyverse`, `dplyr`, `readr`, `tidyr`, `stringr`, `tidytext`, `tokenizers`, `ggplot2`, `gridExtra`,`SnowballC`, `topicmodels`, `quanteda`, `quanteda.sentiment`, `text2vec`, `wordVectors`

These can be installed using `install.packages()` or loaded via preferred package manager. Additional dependencies may be required for replicating the original paper’s Word2Vec embedding or advanced modeling.




<!-- CONTRIBUTORS -->
<h2 id="contributors">Contributors</h2>

<p>
This replication study was completed as part of the Final Project for 
the course PPOL 6801 - Text as Data (Spring 2025) at 
<a href="https://mccourt.georgetown.edu/">Georgetown University, McCourt School of Public Policy</a>.
</p>

We gratefully acknowledge the original authors for publicly sharing their data and code, which made this replication possible. We also appreciate Professor Nejla Asimovic for her invaluable guidance and support throughout the project.

<ul>
  <li><strong>Tian Tong</strong> - <a href="mailto:yt583@georgetown.edu">yt583@georgetown.edu</a></li>
</ul>

