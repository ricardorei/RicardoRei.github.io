* [Home](../index.md)

# Regular Expressions 

> Text by: [Luísa Coheur](authors.md)

I'm sure that you have heard about Regular Expressions (RE). Here
we will use a very informal definition: a RE is just a pattern that describes
sequences. You will see how helpful a RE can be in many applications.
Moreover, you will see that we can use them in Vim and Emacs, in a Perl
program and even with a grep.

## Learning to use Regular Expressions

Before we start, here are some things that you should not forget:

* Characters inside braces [] specify a disjunction of characters to match: [ola]pp means "o", "l" or "a" and will match "opp", "lpp" and "app" and not "olapp";
* RE are case sensitive: use [Bb]ola for "bola" and "Bola";
* Instead of [ABCDEFGHIJKLMNOPQRSTUVXWYZ], you can use [A–Z] and instead of [0123456789] use [0-9];
* RE always match the biggest string.

Now some basic stuff:

1. [] and ^ can also be used to declare characters that should not appear in the RE. [^a] means any character, except a;

2. • means any character, ? means zero or one, * means zero or more (the wild card) and + means one or more (always considering what appears before). For instance:
    - a* represents: $$ \varepsilon $$  (empty string), a, aa, aaa, aaaa, ...
    - aa* represents: a, aa, aaa, aaaa, ...
    - [ab]* represents: aaa, abab, bbb, ...
    - [0–9][0–9]* represents all the integers
    - [0–9]+ also represents all the integers
    - ta.*ta matches all the lines in which "ta" occurs twice.

3. ^ indicates the beginning of a line and $ the end of a line
4. \| stands for the disjunction
5. () groups tokens
6. {n} means exactly n occurrences of previous element
7. {n,m} means between n and m occurrences of previous element
8. {n,} means at least n occurrences of previous element
9. \d represents any digit
10. \D means any character that is not a digit
11. \w means any alpha-numeric character or a space
12. \W means any character that is not alpha-numeric
13. \s means any space (tab, blank, ...)
14. \S means any character that is not a space
15. \\*, \\., \? represent, respectively, the special characters *, . and ?
16. \n, \t represent a newline and tab

And now, for something completely different, here goes a brilliant cartoon,
which I hope will inspire your study on RE.

<p align="center">
<img align="center" src="../images/regular_expressions.png"> 
<figcaption> Completely stolen from <a href="https://xkcd.com/208/">https://xkcd.com/208/</a> </figcaption>
</p>


## Some applications based on Regular Expressions

If you have not yet started applying RE you are probably still not convinced
of how useful and expressive they can be. Do you remember talking about
[ELIZA](https://en.wikipedia.org/wiki/ELIZA) in your AI course? Well ELIZA is a computer program that
simulates a psychotherapist. The following is an example of an interaction
with ELIZA:

```
Eliza: How do you do. Please tell me your problem.
you: I'm going to start my Natural Language course tomorrow.
Eliza: Your Natural Languages course tomorrow?
you: yes.
Eliza: Please go on.
you: And I'm stressed about it.
Eliza: Do you know anyone else who is stressed about it?
you: Maybe some of my students.
Eliza: Your students?
you: yes
Eliza: I see.
```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ELIZA was written by Joseph Weizenbaum (MIT) in the mid 60s and
when it appeared, it was taken seriously by many users. The interesting part
is that ELIZA is implemented using simple pattern matching techniques.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;In the following excerpt, you can see some of the patterns that ELIZA
uses. For instance, if I say "I remember the war", this will match with
the first hypotheses and ELIZA would answer one of the following items,
replacing (2) with "the war".

```
decomp: * i remember *
    reasmb: Do you often think of (2) ?
    reasmb: Does thinking of (2) bring anything else to mind ?
    reasmb: What else do you recollect ?
    reasmb: Why do you remember (2) just now ?
    reasmb: What in the present situation reminds you of (2) ?
    reasmb: What is the connection between me and (2) ?
    reasmb: What else does (2) remind you of ?
decomp: * do you remember *
    reasmb: Did you think I would forget (2) ?
    reasmb: Why do you think I should recall (2) now ?
    reasmb: What about (2) ?
    reasmb: goto what
    reasmb: You mentioned (2) ?
decomp: * you remember *
    reasmb: How could I forget (2) ?
    reasmb: What about (2) should I remember ?
    reasmb: goto you
```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Notice however that some implementations are "intelligent" enough to
make some extra processing, and if I say "I remember my cat", instead of
answering "Why do you remember my cat just now?" it answers "Why do
you remember your cat just now?".

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ELIZA was one of the first NLP applications and the first ever chatbot.
You can find many implementations of ELIZA on the Internet. Also, if you
feel the need to talk with ELIZA everyday, please find a real psychotherapist
as soon as you can.


<div>
  <a href="chap_2.html" style="float: left;">❮ Previous chapter</a>
  <a href="chap_4.html" style="float: right;">Next chapter ❯</a>
</div>

<br/><br/>