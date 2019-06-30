* [Home](../index.md)

# N-grams

> Text by: [Luísa Coheur](authors.md)

Until now we have not make use of any linguistic information and in this
chapter... we won't make it either. We will continue our NLP voyage just
by counting stuff, and you will see the amazing things we can do with it.

## N-grams estimation and Markov assumption

Although **N-grams** can be sequences of anything (characters, words, lemmas,
etc.), in this section we will see N-grams as sequences of (N) words.
Therefore, **bigrams** are sequences of two words, **trigrams** sequences of
three words and so on (from now on, to impress your friends and family,
start saying **unigram** instead of "word"). They can be very useful in several
applications in NLP. In this section we will focus on word prediction
and in calculating a sentence probability.

### Word prediction

Can you predict the next word of the following sequences?
1. Once upon a. ..
2. Luke im your ...
3. Vai...
4. Bom...
5. And now for something...

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;What about this?
1. Once upon a time.
2. Luke im your father.
3. Vai chover.
4. Bombóca
5. And now for something completely different.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Now imagine that you want to implement an application that predicts
words. Word predictors can be done with N-grams. Let $$ w_1, ..., w_{n-1} $$ be a
sequence of words (as a notational alternative we will use w_1^{n-1}). If you
want to predict the next word, $$w_n$$, you should try to find the word with
the highest probability of following the given sequence. Therefore, our goal
is to compute the probability of a word $$W$$ ($$= w_n$$), given some history $$ H = w_1, ..., w_{n-1}$$). 
That is, we want to calculate $$ P(W | H)$$. Let us see how to do this.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;As a first hypothesis, let us suppose we have at our disposal a gigantic
corpus with all the sequences in Portuguese (for instance). Let us count
all the observations of the sequence $$HW$$ as well as all the occurrences of
the sequence $$H$$ alone. In this way we can calculate $$P(W | H)$$:

$$P(w | h) = \frac{count(HW)}{\sum_K count(HK)} = \frac{count(HW)}{count(H)} $$

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;As an example, consider that we have:
* H = Once upon a
* W = time

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;In order to calculate $$P(\text{time} | \text{Once upon a})$$, we have to divide the
number of occurrences of _Once upon a time_, by _Once upon a_.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The problem with this formula is the assumption that "we have at our
disposal a gigantic corpus with all the possible sequences in Portuguese". Such thing
is like Santa Claus: it simply does not exists (Please, tell me you knew this.). 
Not even Google has a corpus with all the possible sequences in any language (you certainly have already
asked Google for a certain sequence, between commas, and no result was
found). Ya, sometimes not even the web is big enough to find a certain
sequence of words. So, let us envisage another way of calculating $$P(W|H)$$.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;As you will see, it is not perfect, and, due to that, it perfectly illustrates
something that I want you to learn from this course (if you haven't learnt
it yet). In many scientific fields, models are used in order to explain a
certain phenomena. Here, in NLP, we use many models that we know
that are not perfect to explain a certain phenomenon, but sometimes are
the only **models that respect the commitment between explaining
(most of) the phenomenon in hand and being computationally
tractable**. That is, sometimes we have to adapt ourselves to what we have
at our disposal and live with that (notice that this is valid in science and
also in general life).

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Now is time to remember what a **Markov model** is and what states
the **Markov assumption**. Markov models represent a class of probabilistic
models that assume that we can predict the probability of some future event
without having to look to far in the past; the Markov assumption states that
the probability of a word depends only on the immediately previous ones.
Thus, in order to compute the probability of a word given an history, $$P(W |
H)$$, we will approximate (as I told you) the history by using only the last
words. And if we consider the last word, we will be talking about bigrams,
if we consider the two previous words, trigrams, and so on. That is:

* bigram: 
$$P(W | H) = P(w_n | w_1, w_2, ..., w_{n-1}) \cong P(w_n | w_{n-1}) $$
* trigram: 
$$P(W | H) = P(w_n | w_1, w_2, ..., w_{n-1}) \cong P(w_n |  w_{n-2}, w_{n-1}) $$
* ...

---
**Exercise 16: Using bigrams**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Consider the following corpus, where \<s> represents the beginning of the
sentence and </s> its end (we assume no normalisation):

```html
<s>Eu adoro a Maria</s>
<s>A Maria eu adoro</s>
<s>Eu adoro bolachas Maria</s>
```
...

---

### Calculating a sentence probability

So, we have learnt to estimate the probability of occurrence of a word after
a given sequence. And if now we want to know how probable is a sentence?
Again, as a first hypothesis, we could calculate the probability of sentence
$$w_1^{n-1}$$ by using the **chain rule of probability:**

$$P(w_1^{n-1}) = P(w_1) \times P(w_2|w_1) \times ... \times P(w_n|w_1^{n-1}) = \prod_{k=1}^n P(w_k|w_1^{k-1}) $$


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Nevertheless, we have here the same problem that we had before: we
probably won't be able to calculate stuff like $$P(w_n|w_1^{n-1})$$, because $$count(w_1^n)$$ or $$count(w_1^{n-1})$$ 
(for instance) never occurred. Once again we will use the
Markov assumption and, once again, we can use bigrams, trigrams, etc. to
produce the following estimations:

* bigram: 
$$P(w_1^n) \cong \prod_{k=1}^n P(w_k | w_{k-1}) $$
* trigram: 
$$P(w_1^n) \cong \prod_{k=1}^n P(w_k | w_{k-2}, w_{k-1}) $$
* ...

---

**Exercise 17: Most probable sentence in Portuguese**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Consider unigrams. Which is the most probable sentence in Portuguese,
with 4 words.

---

---

**Exercise 18: Chinese restaurant**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Make (with lots of enthusiasm) the exercise your professor will provide you.

---

## So, how far can we go with N-grams?

N-grams are certainly extremely helpful in many NLP areas, such as Statistical
Machine Translation (SMT), Spell Correction or Speech Recognition.
In SMT, for instance, two types of models are used:

* a Translation Model that is responsible for the semantics of the translation;
* a Language Model, which takes care of the fluency of translations.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;In SMT (and in many other applications) N-grams can be used to build
the Language Model. As an example, consider that you receive the following
sentences as translation candidates of the sentence _Estou cansado_:

* I’m exhausted.
* Tired me.
* I like superman.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The Translation Model should give more points to the second sentence
which is the one that better captures the meaning of the original sentence;
the Language Model will score higher the first and third sentences as these
are more fluent in English. An accurate combination of both models is
essential to reach a good translation engine.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;However, there are some drawbacks in this. In the following we will study
a measure that allows you to make a preliminary evaluation of how N-grams
will fit in your data, and we will briefly talk about the major problems when
using N-grams.

### Evaluating N-grams: perplexity

**Perplexity** is an evaluation metric for N-grams. The idea is the following:
you calculate two probabilistic models (for instance, bigrams and trigrams)
and then you use perplexity to see which one is the better model, that is,
which one has a tighter fit to a corpus or, in other words, which one will make
the corpus more probable. If a model is good it will give high probability to
probable sentences and a low one to "aberrant" ones.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;So imagine that you have calculated the N-grams of your model (bigrams,
trigrams, etc.). Then, considering that your corpus is $$W = w_1^n$$, perplexity
is given by:

$$PP(W) = \sqrt[n] \frac{1}{P(w_1^n)}$$

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Remember that the calculus of $$P(w_1^n)$$ is dependent of the language
model that you are using (based in bigrams, trigrams, etc.). The lowest the
perplexity, the best the model is (being less perplexed is better).
Some years ago, several of your colleagues did a project based on this
concept. The idea was to compare several Portuguese writers in what respects
the N-grams they use in their work. Although it is widely accepted
that perplexity is not the best measure to compare literature, some interesting
results were attained.

### Main problems
One of the major drawbacks with N-grams is that they don’t deal with
long distance dependencies. For instance, the sequence _Gollum loves his
precious_ could be a frequent 4-gram, but if only sentences such as _Gollum
loves in a very sick way his precious_ are found in the text, that 4-gram will
never be captured.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;On the other hand, N-grams, as you can imagine are very dependent of
the corpus where you did your training. Typically, best results are obtained
by increasing the values of N, although higher values of N increase the number
of possible N-grams and the resulting tables are each time more sparse
(the data sparseness problem is common in many NLP applications).

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Also, you have probably noticed that if an N-gram does not exists because
it was never found in the training corpus, it will case problems if it is
needed during test, because the associated probability will be 0. A similar
problem arises if an N-gram is extremely unfrequent. There are many techniques
in the literature – the **smoothing techniques** – that deal with this
problem. In this section we will talk very briefly about a few of them. However,
you should understand the main problem: you steal some probability
mass from observable things to given them to non observable events (yes,
like Robin Hood did); thus, you have to recalculate the whole stuff again,
because we are talking about probabilities (their values should be between
0 and 1).

Let us start with the **Laplace Smoothing** or **Add-one Smoothing**.
The value one is added to all frequency counts, that is, we pretend that we
saw each word one more time than we actually did. That is, being V the
vocabulary size (number of the set of tokens), we have, for bigrams:

$$P_{\text{Laplace}}(w_n|w_{n-1}) = \frac{count(w_{n-1} w_n) + 1}{V + count(w_{n-1})} $$

---

**Exercise 19: Add-one Smoothing**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;See what happens when you use Add-one Smoothing in the exercise your
teacher will propose you.

---

Another technique is the **Good-Turing discounting** where the
counts of what was observed once is used to estimate the counts of what
was never seen (other techniques implement this idea).

---

**Exercise 20: Good-Turing discounting**

Check with your professor the probability of having lulas for lunch tomorrow.

---

We can also count with Interpolation, which is a technique that combines
N-grams from different orders to estimate the probability of an N-gram
with 0 frequency, as follows:

$$\hat{P}(w_n|w_{n-2} w_{n-1}) = \lambda_1 P(w_n|w_{n-2} w_{n-1}) + \lambda_2 P(w_n|w_{n-1}) + \lambda_3 P(w_n)$$

In this cases, the training corpus is used to calculate the N-grams and a
development set should be used to calculate each $$\lambda_i$$.

Finally, there are also the so called **backoff** techniques where you move
to lower order N-grams to estimate the probability of an N-gram with 0
frequency.


<div>
  <a href="chap_4.html" style="float: left;">❮ Previous chapter</a>
  <a href="chap_6.html" style="float: right;">Next chapter ❯</a>
</div>

<br/><br/>