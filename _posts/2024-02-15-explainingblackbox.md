---
title: Explaining black box text modules in natural language with language models
authors: Chandan Singh, Aliyah R. Hsu, Richard Antonello, Shailee Jain, Alexander G. Huth, Bin Yu, Jianfeng Gao
year: 2023
published: false
---
2024-02-15, 0944

Status: #paper

Tags: [[Research]], [[Automated]], [[Dictionary Learning]], [[Encoding]], [[fMRI]], [[Interpretability]], [[LLMs]], [[Mech Interp]], [[Transformers]]


#### What *question* do they seek to answer? 
How to better interpret large, opaque LLMs, which has also affected scientific discovery in fields such as neuroscience?

**Why?**
* Opaqueness raises issues with use in medicine, limited capabilities in scientific domains 
* Alignment, safety, blah blah

#### What's their *idea* to answer that question? 
![[Screenshot 2024-02-16 at 1.01.14 PM.png]]
* Summarize and Score (SASC), which produces natural language explanations for text modules
	* text module: any function $f$ mapping text to scalar continuous value (e.g., neuron in LLM, brain region)
* Provides natural language description for what most strongly elicits response from $f$
* 2 main steps
	1. <u>Generate explanation:</u> sorts responses of $f$ to several candidate n-grams $\rightarrow$ *uses LLM to summarize* material of top activating n-grams
	2. <u>Evaluate explanation:</u> use LLM to generate random candidates related and not related to summary $\rightarrow$ then calculate difference in response from $f$ to get **explanation score**!

**What's their contribution?**
* Novel use of LLMs to generate explanations of individual brain regions


#### What *data/models* do they use to test it? 

**Data**:
* "Pre-specified" corpus of text, from which unique n-grams are generated
	* 30 random n-grams and 5 candidate explanations
* 3 settings
	* "Default": n-grams extracted from the corresponding module being tested for summarization
	* "Restricted Corpus": n-grams generated from a single, random corpus for each $f$
	* "Noisy": Gaussian noise with $3\sigma_f$ added to responses from each $f$

**Models**:
* Helper LLM (GPT-3)
##### Why?

**Data**:
* Trade-offs for both size of corpus and n-gram length (due to linearly increasing computation cost for number of unique n-grams)

**Models**:
* Assumes $f$ directly responds to natural language input and can be concisely described by natural language 
	* Also it only explains whatever input it receives, things outside are out of its reach
* 54 synthetic modules constructed from pre-trained Instructor model 
	* Each uses distinct dataset that has simple description (*ground truth!*)

#### What *experiments* do they run? Pick main ones.
1. Check accuracy of SASC in being able to recover the ground truth explanations (and compare across varying models, n-gram lengths)
2. Compare explanation score of SASC to that of human-given explanations using BERT Transformer factor modules
	* *BERT transformer factor modules*: Transformation of activations learned via dictionary learning across layers
		* Input: Text sequence
		* Output: Scalar dictionary coefficient (which are human-interpretable)
3. Generate SASC explanations for 1500 *well-predicted* voxel modules (evenly across 3 subjects and diverse cortical areas)
	* Modules fit to voxel activity using text embeddings from pre-trained LLaMa

##### **Why?** 
1. Check summarization capabilities across different settings
2. Measure reliability of summarization vs. other metrics
3. Generate explanations for explaining activity in the brain 

#### What else would *I* like to see?

  

  
#### What do their results say (*my* interpretation)? Same ones.
1. Tables 1 & 2![[Screenshot 2024-02-15 at 10.41.29 AM.png]]
	  * Not much variation by changing the n-gram length or LLM backbone used
	  * Default performance is best 
  2. Table 4![[Screenshot 2024-02-15 at 10.48.56 AM.png]]
	* The SASC explanations are often *better* 
		* However, this explanation score seems a little unfair since the summarization is generated by an LLM and synthetic candidates used for scoring are *also by an LLM*
		* Whereas in the human case it's an LLM building off of a what a human wrote
3. Figures 3 & 4![[Screenshot 2024-02-15 at 10.56.50 AM.png]]
	* Explanation scores often lower for the brain areas than for the BERT layers
	* Also BERT layers explanation scores tend to go down as the layer increases, potentially hinting that it's not as simple?

#### What do their results say (*their* interpretation)? Same ones.
1. Table 1 & 2
2. Table 4
	* No manual effort required and explanations are often as good as human-provided ones
3. Figure 3 & 4
	* Sometimes explanations are able to capture the known selectivity of brain areas
	* Also possible to generate more fine-grained explanations for the brain regions than before (*sort of builds upon decoding work...*)
	* Voxels tend to encode social words and perceptual words 
  


#### What are their conclusions?
1. Builds upon interpretability work and using deep learning for explaining representations in brain
2. Could enable *better* mechanistic interpretability for LLMs and the brain (finer detail)

##### **Any future directions to extend?**
1. How could this be extended to decoding work?
2. SASC doesn't capture anything beyond n-gram information (e.g., low-level textual data)
	* [[MEG]]?
3. Explains modules in isolation, how to explain circuits of modules together?
	* How would this even look?

