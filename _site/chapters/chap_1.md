* [Home](../index.md)

# What? Why? Who? Where?

> Text by: [Luísa Coheur](authors.md)

## What does Natural Language mean?

Let us start by making sure that you understand what NL means. You can find many definitions in the literature, but in my opinion, the concept can be clearly understood if the following semantic is given to the words “Natural” and “Language”:
* The word “natural” expresses the natural evolution due to people communication.
* The word “Language” means a grammatical system (that is, with its own rules) that is used to communicate.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;In fact, there are new words emerging everyday, as for instance _kunami_, _troikiano_, _stressar_, _sanita_, _quispo_. Some of these words die after some time, others are officially recognized and added to dictionaries. A good example is the word _stressar_, which is currently in the [Priberam’s dictionary](http://www.priberam.pt/dlpo/). It should also be clear that there are some rules controlling what can be said. For instance, you can say Eu adoro as aulas de Língua Natural, but not *aulas eu Língua Natural as adoro.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;So, Portuguese and English are NLs and C++ is not (there is “no natural evolution due to people communication” within programming languages). However, the distinction is not that simple: what about Esperanto? Esperanto, created by Ludwig L. Zamenhoff (a Polish physician) in 1887, is the most commonly used “natural artificial” (or “artificial natural”) language. It has the advantage of having an extremely regular grammar (for instance, there are no irregular verbs) and of keeping a simple relation between written/spoken text (for each letter there is one single sound), which leads to a faster learning. Esperanto’s vocabulary came mostly from Romance languages (a minor part came from Germanic languages, English and Slavic languages). It was artificially built, but it has had a natural evolution though time. Therefore, it is a NL or not? Well, some people consider Esperanto as a NL and other people don’t. Google will show you many opinions on this subject and will also show you other constructed languages such as *Ido* and *Interlingua*. To conclude, although not leading to so much discussion, what about Frantuguês? There is a dictionary
already available!

<p align="center">
<iframe width="560" height="315" src="https://www.youtube.com/embed/_jPufypajn8" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</p>

## Why is it so diffcult to deal with Natural Language?

NLs are definitely difficult to deal with, some being more complicated than others. For instance, Portuguese possesses much more specific verb tenses than English does thus, the conjugation of verbs is more complex. The existence of *agreement between words* is also a source of problems in many languages. For instance, in Portuguese, nouns and adjectives have to agree, which is not the case in English. In German, besides the _Masculine_ and _Feminine_, there is also the gender _Neuter_. As we will see throughout this course, there are NL with very strange rules.


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Nevertheless, despite the fact that some NLs are particularly complex, all of them share the same two main problems, which are the ones that make them so difficult to deal with from a computational point of view:

* Linguistic variability: the possibility of expressing the same thing in many, many, many, many, many, many, many, many, many, many different ways.

* Ambiguity: the fact that words/expressions/sentences have several meanings (which leads to the biggest mess in the world).

---
**Exercise 1: Linguistic variability 1**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Try to find 10 ways of saying that you adore your NL courses. You will see that it is not that difficult to find 10 alternative sentences, but many more exist (by the way: instead of alternative sentences, use from now on the word paraphrase. I’m sure your friends will be quite impressed).


**Exercise 2: Linguistic variability 2**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Imagine that you are building an agent that answers questions about your university. Write a list of FAQs that the agent should be able to answer and then write all the paraphrases of each question in the FAQs list that you can imagine. Abort the process eventually.

---

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Considering ambiguity, this is the main characteristic that makes NL and artificial languages so different. Just to give you a brief idea how ambiguous is your own language (in case you haven't noticed yet), consider the following sentences:

1. Encontramo-nos no banco ao lado do quiosque.
2. Cuidado com o Degrau!
3. O Pedro viu o homem na montanha com o telescópio.
4. Quero um hotel com piscina que tenha água quente.
5. Quero um hotel com piscina que tenha suite nupcial.
6. O general bateu a bota.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The word _banco_ is ambiguous: it can be that thing where you can sit or the place where you can put your money. The word _Degrau_ is not ambiguous, but if somebody tells you that Degrau is the name of his/her dog, the meaning of the sentence completely changes. We call this lexical ambiguity (notice that the fact that it starts with a capital letter can give you a clue that it is not being used in the usual way).

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The third situation is a classic example of what we call syntactic ambiguity, because the main problem is the relation between the syntactic constituents and how to connect them. Who had the telescope? Pedro or the man in the mountain? The man was in the mountain or it was Pedro who was in the mountain? This case also illustrates a complicated phenomena, known in NLP as the PP-attachment problem (stands for prepositional phrase), where the machine should be able to identify to which phrase the PP is attached. However, other constituents can also pose a similar problem. This is the case of examples 4 and 5. In the first case the relative sentence que tenha água quente is almost sure related with piscina and, in the second case, que tenha suite nupcial is related with hotel. You should understand that the main problem is that we, humans, are able to decide that some interpretations are possible and others aren’t; however, it is very difficult to make the computer understand which are the correct interpretations. 

---
**Exercise 3: Syntactic Ambiguity**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Try to find all the interpretations of the sentence "O Pedro viu o homem na montanha com o telescópio".

---

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Finally, consider the sentence _O general bateu a bota_. As _bateu a bota_ is an *idiomatic expression* that means _to die_, from that sentence we are not able to understand what happened with the general. As this sentence can be understood both ways – literally and figuratively – it is an ambiguous idiomatic expression.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The main problem with ambiguity is that sometimes even informations source that should be 100% clear, are ambiguous. For instance, consider the sentence (taken from a Portuguese newspaper):

> _Espanha: Portugal será o último país da UE a recorrer à ajuda externa._

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The first time I read it, I thought that Spanish people were saying that Portugal would never ask for help, that is, we would be the last country in the world that would ask for help (ya, I'm so naive). Then, I understood that they were saying that we would really be the **last** country asking for help, because they would never do it (ya, they are also pretty naive).

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;In fact, if during one single day, you keep close attention to what people tell you (even teachers/professors), you will see the incredible doses of ambiguity that we produce everyday. However, as you will see, the majority of situations can be disambiguated, mainly due to the **context** in which they occur, as you can see in the following examples. Notice that, once again, while it may be easy for you to understand what is now the correct meaning of each one of the previous examples, it is extremely difficult to teach a computer to do it.

1. Encontramo-nos no banco ao lado do quiosque. Aquele que tem um multibanco na entrada.
2. Cuidado com o Degrau! Morde que se farta.
3. O Pedro viu o homem na montanha com o telescópio. O homem estava a nadar costas no lago<span id="a1">[[1]](#f1)</span>.
4. O general bateu a bota. Conseguiu assim sacudir a pedra que o estava a magoar.


Nevertheless, it is not only the textual context that helps to disambiguate a sentence. Consider the sentence _O professor não corrigiu um exame!_ and
try to say it loud with the two following meanings: in the first, the teacher corrected all the exams, except one; in the second, the teacher did not correct a single exam. Strange, isn’t it? An innocent sentence with two different meanings that depend on how it is said. In fact, this is not so unusual if we think about, for instance, irony. This opens many possibilities to the meaning of almost any sentence. Even a simple _Bom dia para ti_ can have different semantics, depending on the way it is said.

To conclude, let us define the literal meaning of a sentence to be its default meaning, ignoring context. As we will see, in many scenarios we only deal with literal meaning as context is extremely difficult to code. We will deeply study this concept when we approach the semantic level of language.

## Who are the brave people that work in NLP?
<p align="center">
<img align="center" width="269" height="355" src="../images/brave.png"> 
</p>

In Portugal there are many research centers working in NLP, including
the one from [INESC-ID (L2F)](https://www.l2f.inesc-id.pt/w/Welcome_to_the_Spoken_Language_Systems_Lab). In fact there are research centers at Porto,
Aveiro, Minho, Algarve, Evora and in companies such as [Unbabel](https://unbabel.com/),
[Priberam](http://www.priberam.pt/) and [Microsoft](https://www.microsoft.com/en-us/research/group/natural-language-processing/). In the rest of the world there are many and many
groups working in NLP. Recently, Jurafsky (the author of the [book](https://web.stanford.edu/~jurafsky/slp3/)
that I recommend for this course and from which this material is strongly
inspired) decided to give on-line NLP courses. These courses – that I also
highly recommend – engaged more than 40.000 people (just search for them
in the internet – not the people, the courses<span id="a2">[[2]](#f2)</span>).

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;You can find people with different backgrounds working in NLP. 
If you take a look at L2F, you will find people from Computer Science, Electronic
Engineering and Linguists. A psychologist would also be more than welcome
to help us understand feelings/emotions/personalities, as this is strongly
related with the way people express themselves (remember that NL is only
one of the things we use to communicate; gestures and facial expressions are
also used in the communication process).

## What about the involved knowledge?

In fact, having people with different backgrounds in a research group can be
a big advantage. For instance, linguists study, analyze and dissect language
until exhaustion. Some computer scientists profit from their knowledge to
create their symbolic (rule-based) models/tools. However, it is also true that
other computer scientists completely ignore linguists and use other weapons
against NL: Statistics/Machine Learning. For instance, in applications such
as Machine Translation, statistical approaches win and sometimes very little
linguistically motivated sources of information lead to amazing results.
Sometimes, even the most polluted ones offer interesting results (have you
ever looked at a phrase table in Statistical Machine Translation?). However,
the control of different types of knowledge is certainly very important
in this field and there are many hybrid systems combining linguistic information
with statistics and Machine Learning techniques.
In the following we will talk about the different types of knowledge involved
in NLP:

* **Phonology:** studies the relation between words and sounds. For instance, try to say the word _almoço_. You don't know how to say it, do you? This is because it sounds differently if you say _Hora do almoço_ or _Hoje almoço tarde_.

* **Morphology:** related with words and its units of meaning. Here is where we dissect words (ex: gat+o/os/a/as) and understand how important are some of their constituents for some applications.

* **Syntax:** studies how words can be put together in order to originate sentences. We will review some of the concepts that you have learned in the Compilers course, namely the concept of grammars. We will also study several algorithms for syntactic analysis. Hope that at the end of this chapter you will be totally convinced that NLs are much more complicated than the formal languages you have been studying in the past.

* **Semantics:** respects the study of (the literal) meaning. This is the level of information where everything turns to be almost impossible to control in NLP. Do you remember in LP or IA when you were using First Order Logic to represent the meaning of a sentence? Now try to do that automatically... for all sentences in your own language (if you succeed, don’t forget to tell me how you did it). We will take a look on the main efforts and we will learn about some interesting sources of information that can help improving many NLP applications.

* **Pragmatics:** studies how the context contributes to the meaning.

* **Discourse:** study of language beyond the sentence boundaries. When we read a text, an object is not always referred to in the same manner. Thus, in order to understand the text, we need to be able to follow the different denominations of an object, that is, to establish its coreferences (ex: _John loves his brother. He is so nice._).

* **Knowledge about the word:** to allow inferences. (ex: murder and to kill mean the same in some contexts).

It is a fact that in NLP more knowledge means more possibilities, but
sometimes it is difficult to integrate different forms of knowledge. You can
find in [Linguateca’s page](http://www.linguateca.pt) many linguistic resources for Portuguese.

## Which are the main weapons used in NLP?
There are techniques, formalisms, tools and linguistic resources that
are extremely important in NLP. Here follow some that we will study during
this course:

* Regular expressions;
* Transducers;
* Edit distances;
* HMMs;
* Context free grammars;
* WordNet;
* Neural Networks
* ...

It should be clear that there are tools for almost everything in NLP.
My advice: don't implement your own morphologic analyzer or syntactic
parser. Somebody already did it and you are just wasting your time. The only
reasons I can accept for implementing an existing tool are the following: a)
the existing tool is really bad; b) the existing tool is a black box, and you
need to have control of some of its internal behaviour.

## Can you give me some examples of NLP applications?

People working in NLP are trying to create computational models that can
be used in the many involved problems they have at hands. There are so
many targets that it is difficult to enumerate all of them. Here follow some
applications that you probably heard about:

* Google Translator;
* Siri;
* Watson;
* Wolfram Alpha.

Involved in these systems are research areas such as:

* Speech Recognition/Synthesis: allow you to transcribe what is said and to transform text into speech, respectively.
* Speech/Natural Language Understanding: allows you to understand what was said.
* Machine Translation: translation systems. These can also take speech as input and return speech in the output (Speech-to-Speech Machine Translation).
* Dialogue Systems: systems with which you can talk to in order to ask for information or make them do some task for you (reserve tickets, switch on/off the TV, etc.);
* Question/Answering (QA): systems that contrary to search engines, accept queries in NL (also called questions :-)) and try to return the exact answer to that question (and not a set of documents where the answer may be found);
* Sentiment Analysis: systems that analyze the polarity of some text. They can help you, for instance, to decide to buy a book (or not), as some of these systems analyze people comments about a certain item (a car, a book, a computer, a politician, etc.) and tell you if the general opinion is positive or not;
* Summarization: they make resumes of texts (ya, it would be great to have such system summarizing your NL course book);


### Footnotes
1. <span id="f1"></span> Still ambiguous! [>](#a1)
2. <span id="f2"></span> See what an anaphoric ambiguity can do? :-) [>](#a2)

<div>
  <a href="chap_2.html" style="float: right;">Next chapter ❯</a>
</div>

<br/><br/>