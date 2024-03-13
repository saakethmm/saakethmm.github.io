---
title: Semantic reconstruction of continuous language from non-invasive brain recordings
authors: Jerry Tang, Amanda LeBel, Shailee Jain, Alexander G. Huth
year: 2023
published: false
---
2024-02-10, 1104

Status: #paper

Tags: [[Research]], [[fMRI]], [[Beam Search]], [[Language]], [[Generative model]], [[Decoding]], [[Encoding]], [[BCIs]], [[Computational Neuroscience]]

#### What *question* do they seek to answer? 
Typical BCIs require intracranial recordings to restore communication. The study aims to answer 2 questions:
1) Is it possible to use non-invasive recordings to decode continuous language? 
2) In particular, how do we overcome the limited spatial/temporal resolution of neural activity?

**Why?**
For those who can't speak, non-invasive decoding could be *huge*. Also, this has the potential to be used for augmentative purposes (e.g., decoding thought). 

#### What's their *idea* to answer that question? 
* Construct a decoder that takes in fMRI as input and reconstructs perceived & imagined stimuli using continuous natural language 
* But this is an ==*ill-posed*== problem (due to fewer images compared to word sequences)!
	* Instead generate candidate word sequences and score the likelihood $\rightarrow$ select best candidate
	* How to compare word sequences to brain responses?
		* Use an encoding model using *semantic features* to predict brain from natural language (allows generation of predicted response from word sequence)
		* Likelihood of word sequence evoking particular response can then be compared against the actual response
	* ==But how to pick word sequences?==
		* Use a generative LM to predict words that could come next (to mimic natural language rather than use all combinations...)
		* Use *beam search algorithm* to further refine (where previously generated words continually used as context)

**How do they come up with it?**
Ill-posed problem, which requires the use of some additional priors, which comes in the form of the generative LM.

#### What *data/models* do they use to test it? 

**Data**:
* 16h of fMRI data

**Models**:
* Encoding model based on semantic features
* Decoding model using encoding weights to get similarity scores
	* Predictions generated by LM

**Why?**

#### What *experiments* do they run? Pick main ones.
1. Schematic of their approach![[Screenshot 2024-02-10 at 4.26.40 PM.png]]
	* Decoding model trained for 3 different subjects and evaluated on separate brain recordings from a novel test of stories 
2. Another interesting question to ask is what information each language region contains - so 3 regions tested using decoder approach (speech network, parietal-temporal-occipital association region, prefrontal region) and how this compares to the whole brain

**Why?** 
1. Generative LM needed to pick out logical phrases to then pick max likelihood over
2. Unclear which regions represent language at the level of words/phrases 

#### Would *I* run different experiments? What else would *I* like to see?

None come to mind atm  

  
#### What do their results say (*my* interpretation)? Same ones.
1. Figure 1![[Screenshot 2024-02-10 at 3.32.42 PM.png]]
	* Very interesting to observe that the actual sentences and predicted sentences have similar meanings, where the decoded words sometimes use the exact same words
	* In 1f, the similarity at intervals along the entire stimulus is quite clearly seen which is very promising
2. ![[Screenshot 2024-02-10 at 4.39.46 PM.png]]
	* The similarity at the level of words is actually quite present throughout all the major regions of the language network 
	* Even across meaning, a lot of similarities are shared (as seen by high BERT score) across regions
3. Figure 3![[Screenshot 2024-02-10 at 6.13.05 PM.png]]
	* Fascinating results where there is indeed a strong semantic relationship between *imagined* stories and decoded stories 
#### What do their results say (*their* interpretation)? Same ones.
1. WER, BLEU, METEOR all measure number of words shared by two sequences (in some rough sense), while BERTscore measures something more semantically meaningful (using BERT) 
2. Figure 2
	* **2c**: Association & PFC both captured similar similarity scores (by significance) compared to the whole brain, though the *speech* network notably did not perform the same (likely due to speech network encoding lower-level auditory features)
	* **2d**: Direct comparison between decoded word sequences, which shows that different cortical regions encode redundant word-level representations 
		* ***Crucial Question***: how they could be encoding these words (i.e., with what features), could be totally different!
3. Figure 3
	* **3c**: Very interestingly, even across modalities (in this case vision with no sound) the semantic decoder can actually be used to figure out what's going on in the movie
	* **3d**: When attending to particular speakers (Female or Male), the decoding accuracy is much higher for the one being attended (for privacy, shows that only attended to object is what can be decoded accurately)


#### What are their conclusions?
* Main challenges: limited data, incorrect semantic features extracted, noisy signal
* Proof of concept that meaning of perceived and imagined speech can be decoded into continuous language!
	* Very clever use of LLMs
* Demonstrates that fMRI BOLD signals contain semantic information even at the level of the word
	* This semantic information is arguably more useful across modalities than what can be used of motor information
* Invasive decoding does not necessarily improve exact word recovery compared to non-invasive decoding 
* Performance of decoder could be improved using combined motor + semantic features (e.g., MEG with precise timing information)


**Do they make sense?**
Yes.

