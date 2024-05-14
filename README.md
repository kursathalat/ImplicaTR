# ImplicaTR
ImplicaTR is an NLI dataset that improves the conventional entailment-neutral-contradiction classification of NLI tasks with the scalar implicatures. Thus, ImplicaTR offers further investigation of the pragmatic capabilities of LLMs.

ImplicaTR was semi-synthetically created originally in Turkish and comes also in English, translated with Gemini Pro 1.5 through "guided-translation".

There is also a base version of ImplicaTR, on top of which ImplicaTR was created; more info xx

Thus, this repo features four versions of ImplicaTR:

- ImplicaTR: The main version of ImplicaTR in Turkish
- ImplicaTR-EN: The English version of ImplicaTR

- ImplicaTR-base: The base version of ImplicaTR in Turkish
- ImplicaTR-base-EN: The base version of ImplicaTR in English


# What is ImplicaTR?

ImplicaTR is an NLI dataset which offers more granular classification of the inferences between two sentences by incorporating the linguistic phenomenon of scalar implicatures. How the dataset was created is given in the Base Version section below. The number of rows is 19,350 and it is split into 3 parts:

- Train: 12,309
- Validation: 3,153
- Test: 3,888

Each row is also annotated with the linguistic features:

- Linguistic category of the scalar item: Adjectives, Verbs, Quantifiers, Modals, Numerals, Partitives
- The set number of the sentence within its linguistic category
- The sentence number of the sentence within its set
- The scalar pair

Labels:
- 0: entailment
- 1: neutral
- 2: contradiction
- 3: implicature

Partitives are not given in the main version of ImplicaTR but given extra in the same folder. This is because they alter the entailment-implicature relationships of the between the premise-hypothesis pairs.

| Linguistic Category | N of scalar pairs | N of sets per scale | N of rows per set | Total N of sets | Total N of rows |
|---|---|---|---|---|---|
| Adjectives | 15 | 30 | 8 | 450 | 3600 | 
| Verbs | 9 | 50 | 8 | 450 | 3600 | 
| Quantifiers | 9 | 50 | 8 | 450 | 3600 | 
| Modals | 2 | 225 | 8 | 450 | 3600 | 
| Numerals | 9 | 50 | 11 | 450 | 4950 | 
| Partitives (given extra) | 9 | 10 | 11 | 90 | 900 |

The train, val and test sets were created by means of the base version with stratified sampling. Thus, the classes are balanced in the train, val and test sets.

Translation of ImplicaTR into English was done with Gemini Pro 1.5 with "guided-translation". Guided-translation pipeline is as follows: each set from each linguistic category was seperately fed into the LLM with proper prompts. In these prompts, the scales were explicitly given with their translations and the LLM was asked to translate the sentences strictly obeying these translations.

An example set of sentences from ImplicaTR (with ImplicaTR-EN version in parentheses):

| Linguistic Category | Set Number | Sentence Number | Scalar Pair | Premise | Hypothesis | Category | Label |
|---|---|---|---|---|---|---|---|
| 4 | 96 | 1 | muhtemelen-kesin (probably-certain) | Bu şarkıyı muhtemelen dinlerim. (I will probably listen to this song.) | Bu şarkıyı dinleyeceğim kesin değil. (It is not certain that I will listen to this song.) | implicature | 3 |
| 4 | 96 | 2 | muhtemelen-kesin (probably-certain)  | Bu şarkıyı dinleyeceğim kesin değil. (It is not certain that I will listen to this song.) | Bu şarkıyı muhtemelen dinlerim. (I will probably listen to this song.) | implicature | 3 |
| 4 | 96 | 3 | muhtemelen-kesin (probably-certain)  | Bu şarkıyı muhtemelen dinlemem. (I probably won't listen to this song.) | Bu şarkıyı dinleyeceğim kesin değil. (It is not certain that I will listen to this song.) | entailment | 0 |
| 4 | 96 | 4 | muhtemelen-kesin (probably-certain) | Bu şarkıyı dinleyeceğim kesin. (It is certain that I will listen to this song.) | Bu şarkıyı muhtemelen dinlerim. (I will probably listen to this song.) | entailment | 0 |
| 4 | 96 | 5 | muhtemelen-kesin (probably-certain) | Bu şarkıyı dinleyeceğim kesin değil. (It is not certain that I will listen to this song.) | Bu şarkıyı muhtemelen dinlemem. (I probably won't listen to this song.) | neutral | 1 |
| 4 | 96 | 6 | muhtemelen-kesin (probably-certain)  | Bu şarkıyı muhtemelen dinlerim. (I will probably listen to this song.) | Bu şarkıyı dinleyeceğim kesin. (It is certain that I will listen to this song.) | neutral | 1 |
| 4 | 96 | 7 | muhtemelen-kesin (probably-certain)  | Bu şarkıyı dinleyeceğim kesin. (It is certain that I will listen to this song.) | Bu şarkıyı muhtemelen dinlemem. (I probably won't listen to this song.) | contradiction | 2 |
| 4 | 96 | 8 | muhtemelen-kesin (probably-certain)  | Bu şarkıyı muhtemelen dinlemem. (I probably won't listen to this song.) | Bu şarkıyı dinleyeceğim kesin. (It is certain that I will listen to this song.)| contradiction | 2 |


# What is the Base Version?

The base version is the original database where each set of sentences were created within specific categories and sets. Then, depending on the [Square of Opposition](https://en.wikipedia.org/wiki/Square_of_opposition), the sentences from each set were combined to reveal the entailment, neutral, contradiction, and implicature labels. The base version also includes the implicature tests proposed in the linguistic literature. These sentences also offer pieces of data for finer analysis of the pragmatic capabilities of LLMs. The tests included are the cancellation, suspension, reinforcement tests.

A sample set is given in the table below:

| column | ImplicaTR-base | ImplicaTR-base-EN |
|---|---|---|
| scale | muhtemelen-kesin | probably-certain |
A|Bu şarkıyı muhtemelen dinlerim. | I will probably listen to this song. |
B|Bu şarkıyı dinleyeceğim kesin. | It is certain that I will listen to this song. |
C|Bu şarkıyı muhtemelen dinlemem.  | I probably won't listen to this song. |
D|Bu şarkıyı dinleyeceğim kesin değil.| It is not certain that I will listen to this song. |
AD_Cancellation |Bu şarkıyı muhtemelen dinlerim, hatta dinleyeceğim kesin.| I will probably listen to this song, in fact, it is certain that I will listen to it. |
AD_Suspension | Bu şarkıyı muhtemelen dinlerim, dinleyeceğim belki de kesin.| I will probably listen to this song, and it may be certain that I will listen to it. |
AD_Reinforcement | Bu şarkıyı muhtemelen dinlerim ama dinleyeceğim kesin değil.| I will probably listen to this song, but it is not certain that I will listen to it. |
DA_Cancellation | Bu şarkıyı dinleyeceğim kesin değil, hatta muhtemelen dinlemem.| It is not certain that I will listen to this song, in fact, I probably won't listen to it. |
DA_Suspension | Bu şarkıyı dinleyeceğim kesin değil, muhtemelen dinlemem bile.| It is not certain that I will listen to this song, I probably won't even listen to it. |
DA_Reinforcement | Bu şarkıyı dinleyeceğim kesin değil, ama muhtemelen dinlerim.| It is not certain that I will listen to this song, but I will probably listen to it. |

ImplicaTR is created on the A, B, C, and D sentences: entailment -> C-D and B-A, neutral -> D-C and A-B, contradiction -> B-C and C-B, implicature -> A-D and D-A. AD and DA in the test names indicate for which pair the test is applied.


# Creative Commons License

This dataset is made available under a Creative Commons Attribution-ShareAlike 4.0 International License (CC BY-SA 4.0), which allows you to use the data as long as you give appropriate credit to the original author and share any derivative works under the same license.

# Citation

Upcoming paper

If you use ImplicaTR in your research, please cite as follows:

```
@misc{implicatr,
  title={ImplicaTR: An NLI Dataset with Scalar Implicatures},
  author={Halat, Mustafa Kürşat},
  journal={GitHub repository},
  year={2024},
  publisher={GitHub},

}
```