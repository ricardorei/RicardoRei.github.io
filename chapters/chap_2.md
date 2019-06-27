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

<div>
  <a href="chap_1.html" style="float: left;">❮ Previous chapter</a>
  <a href="chap_3.html" style="float: right;">Next chapter ❯</a>
</div>

<br/><br/>