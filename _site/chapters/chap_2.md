* [Home](../index.md)

# Methodology, corpora and evaluation

> Text by: [Luísa Coheur](authors.md)

Depending on the problem at hand, your framework will vary. However,
there are some elements that are common in almost every research in NLP.
For instance, the way you should deal with your data, so that your experiments
are considered to be sound, and the evaluation metrics you will use.
In this section we will discuss this issues.

## The scientific method

Do you remember studying the scientific method in biology, when you were
a kid? According to the Merriam-Webster dictionary, a scientific method
consists of:

> "The collection of data through observation and experimentation, and the formulation and testing of hypotheses".

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;In order to explain different phenomena, scientists suggest hypotheses,
and design experiments to test them. In NLP you should also follow the
scientific method. First, you should know something about the phenomena
that is the target of your research and you should be able to perfectly identify
the goals of your work and the hypothesis that you want to test. Then you
should think on how you will test this – which architecture, which corpora
(corpora is the plural of corpus and no, it doesn’t mean "dead body"), which
metrics, which tools – and design the experiments that will corroborate (or
not) your point (remember that if you change more than one variable at
the same time, you will not be able to understand what was responsible
for the attained results). Then you implement the system that will allow
you to run your experiments, you will run it, you will evaluate the results
using (known) evaluation metrics and you will see if your hypothesis still
rules. If it does, perfect, you made your point. If it doesn’t, don’t cross your
arms, you should try to understand what went wrong (make a detailed error
analysis – results don’t bite) and reformulate your hypotheses. Notice that
not having a good result may also be interesting: if your hypothesis is well
justified, I’m sure many people will want to know about it. Also notice that
if similar systems also report results, you should run your experiments with
the same data, so that you can make a straightforward comparison with
them. This is exactly the process that I want you to follow in this course
(this is really important).

## Corpora

### Building corpora

One of NLP researchers’ best friends are corpora. Regardless of whether
your research falls into a symbolic or a statistical approach, corpora are
always welcome. However, collecting corpora and processing it, so that
it can be used for training or testing, is a time consuming and expensive
task, that sometimes can only be done by experts (would you be able to
label a text with the morpho-syntactic category of each word? Well... me
neither). Many efforts were done in recent years and there are many corpora
at your disposal, as well as many annotation guidelines, which can be used
depending on your application needs (Brown Corpus, Floresta Sintáctica,
Público, etc.). There are also organizations that centralize many corpora and
sell them (see for instance the European Language Resources Association
(ELRA) or the Linguistic Data Consortium (LDA) webpage). Recently,
many researchers have been using the [Mechanical Turk](https://www.mturk.com/) and many people
from the NLP community are using "Requesters" to create several types of
corpora.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Nevertheless, it might happen that you will have to build your own
corpora for your experiments (at least for testing your application). If so,
take some time to think how you will do it and don’t neglect this task, as
the success of your work is highly dependent on it.

### Inter-annotator agreement
The concordance among raters (also called inter-rater reliability or interrater
agreement) tells you how much consensus there is in the ratings given
by judges on some task. For instance, consider that I give you a text and
tell you to classify a set of answers of a virtual agent as being appropriate or
not, in a scale from 1 to 10. Consider also that I propose the same exercise
to a friend of yours. Then, I will see how much agreement there is between
you. If the degree is low, either the scale is defective or you need to be
trained in doing such job. There are many statistics which can be used to
determine inter-annotator agreement. An example of one such measure is
the [Cohen’s kappa coefficient](https://en.wikipedia.org/wiki/Cohen%27s_kappa), as defined in following Equation:

$$K = \frac{P(a) - P(e)}{1- P(e)}$$

where:
* $$P(a)$$ is the relative observed agreement among raters;
* $$P(e)$$ is the probability of random agreement (during class I will explain how to calculate this value).

As an example, consider that two annotators have to classify some questions
with A, B or C, and that Table 1 summarizes the inter-annotator
agreement results.

|  | A | B | C | Total |
| :-- | :-----------: | :-----------: | :-----------: | ----: |
| A | 15 | 0 | 0 | 15 |
| B | 1 | 21 | 3 | 25 |
| C | 0 | 0 | 1 | 1 |
| Total | 16 | 21 | 4 | 41 |

Table 1: Inter-annotator agreement.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Annotators agreed on the evaluation of 37 of the 41 questions: 15 A, 21 B
and 1 C. Therefore, the relative observed agreement among raters, $$P(a)$$, is
$$\frac{15 + 21 + 1}{41} = 0.90$$. To calculate the probability of chance agreement,
$$P(e)$$, we need to find the probability that both would say "A" randomly,
the probability that both would say "B" randomly and the probability that
both would say "C" randomly. The former is given by $$\frac{16}{41} \times \frac{15}{41}$$. The
remaining by  $$\frac{21}{41} \times \frac{25}{41}$$ and $$\frac{4}{41} \times \frac{1}{41}$$, respectively. 
Then we sum all the obtained values. $$P(e)$$ is, then, $$0.46$$. Finally, the kappa coefficient (K)
is $$0.82$$.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Now, you are probably thinking if this is good or bad. Well, there is
not much agreement on this, but some authors consider:
* < 0: no agreement;
* 0 – 0.20: slight agreement;
* 0.21 – 0.40: fair agreement;
* 0.41 – 0.60: moderate agreement;
* 0.61 – 0.80: substantial agreement;
* 0.81 – 1: almost perfect agreement.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Thus, the previous result is considered by some authors an almost perfect
agreement (ufa!).

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;To conclude, let me just note that this measure can only be used with
two raters; a similar measure of agreement, called the Fleiss’ Kappa can be
used when more than two raters are involved (and many other measures exist
with this purpose). This is just to give you an idea of what the concordance
among raters is.

### Training, testing and development sets

Regarding the usage of corpora, several restrictions need to be respected if
you want to have a methodologically correct work. So, please, during the
whole course, don't forget the following: divide your corpora in training
and test sets (typically 80%–90% of the corpus is used for training and the
rest for testing – the reference). If you are learning from a corpus or if you
are writing rules for it, you should use the training corpus. Otherwise, when
you evaluate your system you will do so with something that your learning
algorithm or yourself already know, which leads to an unsound evaluation.

---
**Exercise 4: The problem of using the test set for development or training**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Think about this, please.

---

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;If you need to make several tests of your system before the final one
(which is always a good idea), you should take part of your training set
and build a development corpus with it, which simulates the test corpus.
Therefore, before testing your system with the test corpus you can test it
with the development corpus, look at the results, tune your work and test
again with the development set. There is no problem with that. The final
evaluation should be made with the testing corpus that was left untouched
until then.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Notice also that sometimes it is so time-consuming and expensive to
build corpora that only a small collection is built (sometimes called the
gold-collection) and used for testing.


### Cross validation

If you are using your corpus for a learning purpose, you can also not split
it in training/development/testing and, alternatively, make a k-fold cross
validation: you split your corpus into k sets, train your system using k-
1 sets and test it with the remaining one. Usually multiple rounds are 
performed using different partitions and, at the end, the average over the
rounds is returned.

<p align="center">
<img align="center" src="../images/cross_validation.png" width="533" height="293">
<figcaption> Image from <a href="http://karlrosaen.com/ml/learning-log/2016-06-20/">Karl Rosaen Blog</a> </figcaption>
</p>


### The nature of the corpus

There is another thing that you should pay much attention to: the nature
of these corpora needs to be the same for both training and testing,
otherwise you won't be able to conclude much. For instance, it is a really
bad idea to train your system with a corpus of newspapers and then test it
with a book for children; or to learn to identify writers in a poetry corpus
and test the authors' identification in other literature genres.

---
**Exercise 5: The nature of the corpus**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Think about this, please.

---

## Evaluation

One of the first things you will do in your work will likely be implementing
a baseline. The baseline represents the starting point of your system: a
specific configuration with which results are known. Then, you will make
your experiments (add other corpus, change some parameters/algorithms,
etc.) and compare the attained results with the baseline, in order to check
if you are improving them. For instance, if your master thesis comes in
sequence of a previous master, the results obtained by your colleague can
be used as the baseline. Then your work will be to (try to) improve them.

### Extrinsic vs. intrinsic evaluation

If you evaluate your NLP system independently of the context in which it
will be used, you are making an intrinsic evaluation of it; however, if you
evaluate your NLP system as a component of a more complex NLP system,
you are performing an extrinsic evaluation of it. As an example, consider
that you have developed a Question Classifier, that is, a module that tells
you what type of answer should be returned for any question (for instance,
location for Where is Marinhais? or people for Who won the Oscar for
best actor in 2013). When you evaluate how good your Question Classifier
is in returning the correct answer type, you are performing an intrinsic
evaluation of it. However, if you use your Question Classifier within a QA
system, the results of the QA system allow you to extrinsically evaluate
your Question Classifier. What's funny is that sometimes a module with a
(relatively) poor performance can really make an honest contribution when
used in a more complex system.

### Evaluation measures

Another thing that you should know is that, in order to evaluate your work
and/or allow a straightforward comparison with other works, several measures
have been proposed in the literature, some being specific to certain
frameworks. While **precision**, **recall** and **F-measure** are used in many
applications (sometimes with small variations), other evaluation metrics
have specific targets. Thus, **BLEU**, **METEOR** and many others are used
to evaluate machine translation systems, **ROUGE** is used to evaluate
summarization systems and **perplexity** is used to evaluate, for instance
language models (coming soon to a class near you).

Considering the following, we will define precision, recall and F-measure,
as used, for instance, in **Information Retrieval**:

* TP = true positives;
* TN = true negatives ;
* FP = false positives (type 1 errors);
* FN = false negatives (type 2 errors).

Precision is defined as the fraction of retrieved instances that are relevant,
i.e.,

$$\text{Precision} = \frac{TP}{TP + FP}$$

Recall is defined as the fraction of relevant instances that are retrieved,
i.e.,

$$\text{Recall} = \frac{TP}{TP + FN}$$

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Notice that a maximum precision means no false positives and a maximum
recall means no false negatives.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The *F-measure* can be used to combine the above two measures into a
single metric, and it is defined as a weighted harmonic mean of precision
and recall (usually we set $$\beta$$ = 1 (F1)):

$$\text{F}_{\beta} = \frac{(\beta^2 +1) \times \text{Precision} \times \text{Recall}}{\beta^2 \times \text{Precision} + \text{Recall}}$$

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Lets imagine that we have developed a search engine about fruits and vegetables. 
The knowledge-base of our engine only contains information about the following fruits/vegetables:
- Watermellons, Bell Peppers, Large Tomatos, Pomegranates, Bananas, Green Apples, Red Apples, Large Red Apples, Fuji Apples, Yellow Apples, Lemons, Kiwis and Raisins

Consider now the following query:
> red, medium-sized fruits

and the respective system answer:
> Bell peppers, Large Tomatos, Pomegranates, Large Red Apples, Red Apples, Fuji Apples

<p align="center">
<img align="center" src="../images/fruits.png" >
<figcaption> Image from <a href="https://opensourceconnections.com/blog/2016/03/30/search-precision-and-recall-by-example/" width="269" height="355">John Berryman Post</a> </figcaption>
</p>

The precision of our system for that query is:

$$ \frac{3}{3+3} = \frac{1}{2} $$

the recall is:

$$ \frac{3}{3} = 1 $$ 

and finally, the *F-measure* is:

$$ \frac{2 \times 0.5 \times 1}{0.5+1} \simeq 0.667\$$


---
**Exercise 6: Precision vs. Recall**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Consider the following text:

*"The capital of Portugal, Lisbon (Portuguese: Lisboa) has experienced a
renaissance in recent years, with a contemporary culture that is alive and
thriving and making its mark in today’s Europe. Lisbon lacks a defined
"downtown", but the the vast Praça do Comércio, facing the river at the base
of the pedestrianized grid of Baixa (lower town), occupies a central position.
Further northwest from Baixa stretches Lisbon's "Main Street", Avenida da
Liberdade, a broad boulevard resplendent in leafy trees, chic hotels and upscale
shops, terminating at the circular Praça de Marques de Pombal. To the
east are old neighborhoods of Mouraria and Alfama, both relatively spared
during the Great Earthquake (as they are on a firmer rock) and therefore
both retaining the charm of the winding alleys and azulejo-covered crumbling
walls (further north lie relatively boring residential quarters)."* - (taken from [Wikitravel](http://wikitravel.org/en/Lisbon))

and two systems (A and B) that use it for testing their task of extracting locations.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Knowing that system A extracted the locations Portugal, Lisboa, Avenida
da Liberdade and Alfama and that system B extracted Portugal, Lisbon,
Portuguese, Lisboa, Praça do Comércio, Europe, Main Street, Alfama and
Great Earthquake, calculate the recall and precision obtained by these systems.
Which one is better?

---

---
**Exercise 7: Precision better that recall?**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Identify two scenarios where a good precision is more important that a good
recall and vice-versa.

---

Do you remember talking about QA (yes, Question/Answering)? The
Mean Reciprocal Rank (MRR) is a specifically tailored evaluation measure
for QA, as it can be used to evaluate systems that return ranked lists
of possible answers for a given question. For a test set of N questions, the
MRR is given by:

$$ \text{MRR} = \frac{1}{N} \sum_{i=1}^N \frac{1}{rank_i} $$

where $$rank_i$$ denotes the position of the ground-truth answer in the list of candidate answers returned by the system.

Consider the following table:

| Question                          | Ranked list of answers             | Rank | RR  |
| :-------------------------------- | :--------------------------------: | :---:| --: |
| What is the capital of Portugal?  | **Lisbon**, Paço de Arcos, Oporto, Viseu | 1    | 2   |
| When was Mozart born?  | 1884, 1870, 1756, 2012 | 3    | 1/3  |
| Who is the 44th president of the USA?  | B. Clinton, D. Trump, R. Paul, Sampaio | 2    | 1/2   |

with a fictitious run of a QA system for a small test set of three questions. The MRR of such system is:

$$ \frac{1 + \frac{1}{3} + \frac{1}{2}}{3} \simeq 0.61 $$

---
**Exercise 8: Precision and recall – the real problem**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Consider Edgar Smith, the agent that answers questions about
Monserrate. Consider also that if the posed question is outside its domain of
expertise, it should answer *Sorry, can't answer that*. Finally, consider that
its database does not have all the information it needs about its domain.
What will be the TP, TN, FP, FN in this scenario?

---

<p align="center">
<img align="center" width="480" height="386" src="../images/edgar.png"> 
</p>

> Edgar is a tutoring agent at Monserrate palace, Sintra. Click [here](https://www.aclweb.org/anthology/papers/P/P13/P13-4011/) to "Meet" Edgar. 

### Evaluation fora

In order to allow a straightforward comparison between systems, many evaluation
fora take place nowadays (please, take a look at [CLEF](http://www.clef-initiative.eu/) or [TREC](https://trec.nist.gov/)
pages, for instance). Many different tasks are proposed in these fora (QA,
Information Retrieval, Plagiarism detection, etc.) and you only need to register
your system in the ones related with your work. You are given access
to the training data and, at a certain previously scheduled date, the test 
sets are released. Then you have a limited amout of time (some hours, a
week, ...) to send the results of your system to the organizers. After some
time, all the results obtained by the competing systems are divulged and
everybody can see how good (or bad) his/her system is, evaluated in the
same conditions.

<div>
  <a href="chap_1.html" style="float: left;">❮ Previous chapter</a>
  <a href="chap_3.html" style="float: right;">Next chapter ❯</a>
</div>

<br/><br/>