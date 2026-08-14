# Base de Conhecimento

## Dados Utilizados

| Blibioteca | Utilização no Agente |
|---------|----------------------|
| `Open-Web-Math` | Fornece uma grande base de conhecimento pouco estruturado |
| `AMPS` | Utilizar uma metodologia passo a passo para solucionar problemas |
| `GSM8K` | Focado em fornecer raciocínio logico ao agente|
| `Mathlib4` | Utiliza provas rigorosas para realizar o treinamento do agente |
| `Coq Standard Library` | Possui o conteúdo direcionamento a logica e teoria para treinamento do agente |

> [!TIP]
> **Quer um dataset mais robusto?** Você pode utilizar datasets públicos do [Hugging Face](https://huggingface.co/datasets) relacionados a finanças, desde que sejam adequados ao contexto do desafio.

---

## Estratégia de Integração

### Como os dados são carregados

> Descreva como seu agente acessa a base de conhecimento.

Através do python os dados estão sendo carregados e destinados ao treinamento do agente, como no exemplo abaixo:

```python

from datasets import load_dataset

open_web_math = load_dataset("open-web-math/open-web-math", streaming = True)

AMPS = load_dataset("sarahpann/AMPS", streaming = True)
 
GSM8K = load_dataset("openai/gsm8k", "main", streaming = True)

math_lib = load_dataset("phanerozoic/Lean4-Mathlib", streaming = True)
  
coq_stdlib = load_dataset("phanerozoic/Coq-Stdlib", streaming = True)


```

### Como os dados são usados no prompt?

> Os dados vão no system prompt? São consultados dinamicamente?

Os dados não estão sendo utilizados diretamente no prompt, eles estão sendo utilizados através das bibliotecas de datasets do Hugging Face

---

## Exemplo de Contexto Montado

> Mostre um exemplo de como os dados são formatados para o agente.

#### Open-Web-Math
```
Bayes and his Theorem

My earlier post on Bayesian probability seems to have generated quite a lot of readers, so this lunchtime I thought I’d add a little bit of background. The previous discussion started from the result

$P(B|AC) = K^{-1}P(B|C)P(A|BC) = K^{-1} P(AB|C)$

where

$K=P(A|C).$

Although this is called Bayes’ theorem, the general form of it as stated here was actually first written down, not by Bayes but by Laplace. What Bayes’ did was derive the special case of this formula for “inverting” the binomial distribution. This distribution gives the probability of x successes in n independent “trials” each having the same probability of success, p; each “trial” has only two possible outcomes (“success” or “failure”). Trials like this are usually called Bernoulli trials, after Daniel Bernoulli. If we ask the question “what is the probability of exactly x successes from the possible n?”, the answer is given by the binomial distribution:

$P_n(x|n,p)= C(n,x) p^x (1-p)^{n-x}$

where

$C(n,x)= n!/x!(n-x)!$

is the number of distinct combinations of x objects that can be drawn from a pool of n.

You can probably see immediately how this arises. The probability of x consecutive successes is p multiplied by itself x times, or px. The probability of (n-x) successive failures is similarly (1-p)n-x. The last two terms basically therefore tell us theprobability that we have exactly x successes (since there must be n-x failures). The combinatorial factor in front takes account of the fact that the ordering of successes and failures doesn’t matter.

The binomial distribution applies, for example, to repeated tosses of a coin, in which case p is taken to be 0.5 for a fair coin. A biased coin might have a different value of p, but as long as the tosses are independent the formula still applies. The binomial distribution also applies to problems involving drawing balls from urns: it works exactly if the balls are replaced in the urn after each draw, but it also applies approximately without replacement, as long as the number of draws is much smaller than the number of balls in the urn. I leave it as an exercise to calculate the expectation value of the binomial distribution,but the result is not surprising: E(X)=np. If you toss a fair coin ten times the expectation value for the number of heads is 10 times 0.5, which is five. No surprise there. After another bit of maths, the variance of the distribution can also be found.It is np(1-p).

So this gives us the probability of x given a fixed value of p. Bayes was interested in the inverse of this result, the probability of p given x. In other words, Bayes was interested in the answer to the question “If I perform n independent trials and get x successes, what is the probability distribution of p?”. This is a classic example of inverse reasoning. He got the correctanswer, eventually, but by very convoluted reasoning. In my opinion it is quite difficult to justify the name Bayes’ theorem based on what he actually did, although Laplace did specifically acknowledge this contribution when he derived the general result later, which is no doubt why the theorem is always named in Bayes’ honour.

This is not the only example in science where the wrong person’s name is attached to a result or discovery. In fact, it is almost a law of Nature that any theorem that has a name has the wrong name. I propose that this observation should henceforth be known as Coles’ Law.

So who was the mysterious mathematician behind this result? Thomas Bayes was born in 1702, son of Joshua Bayes, who was a Fellow of the Royal Society (FRS) and one of the very first nonconformist ministers to be ordained in England. Thomas was himself ordained and for a while worked with his father in the Presbyterian Meeting House in Leather Lane, near Holborn in London. In 1720 he was a minister in Tunbridge Wells, in Kent. He retired from the church in 1752 and died in 1761. Thomas Bayes didn’t publish a single paper on mathematics in his own name during his lifetime but despite this was elected a Fellow of the Royal Society (FRS) in 1742. Presumably he had Friends of the Right Sort. He did however write a paper on fluxions in 1736, which was published anonymously. This was probably the grounds on which he was elected an FRS.

The paper containing the theorem that now bears his name was published posthumously in the Philosophical Transactions of the Royal Society of London in 1764.

P.S. I understand that the authenticity of the picture is open to question. Whoever it actually is, he looks  to me a bit likeLaurence Olivier…

11 Responses to “Bayes and his Theorem”

1. Bryn Jones Says:

The Royal Society is providing free access to electronic versions of its journals until the end of this month. Readers of thisblog might like to look at Thomas Bayes’s two posthumous publications in the Philosophical Transactions.

The first is a short paper about series. The other is the paper about statistics communicated by Richard Price. (The statistics paper may be accessible on a long-term basis because it is one of the Royal Society’s Trailblazing papers the society provides access to as part of its 350th anniversary celebrations.)

Incidentally, both Thomas Bayes and Richard Price were buried in the Bunhill Fields Cemetery in London and their tombs can be seen there today.

2. Steve Warren Says:

You may be remembered in history as the discoverer of coleslaw, but you weren’t the first.

• Anton Garrett Says:

For years I thought it was “cold slaw” because it was served cold. A good job I never asked for warm slaw.

3. telescoper Says:

My surname, in Spanish, means “Cabbages”. So it was probably one of my ancestors who invented the chopped variety.

4. Anton Garrett Says:

Thomas Bayes is now known to have gone to Edinburgh University, where his name appears in the records. He was barred from English universities because his nonconformist family did not have him baptised in the Church of England. (Charles Darwin’s nonconformist family covered their bets by having baby Charles baptised in the CoE, although perhaps they believed it didn’t count as a baptism since Charles had no say in it. Tist is why he was able to go to Christ’s College, Cambridge.)

5. “Cole” is an old English word for cabbage, which survives in “cole slaw”. The German word is “Kohl”. (Somehow, I don’t see PM or President Cabbage being a realistic possibility. 🙂 )

Note that Old King Cole is unrelated (etymologically). Of course, this discussion could cause Peter to post a clip of

Nat “King” Cole
(guess what his real surname is).

To remind people to pay attention to spelling when they hear words, we’ll close with the Quote of the Day:

It’s important to pay close attention in school. For years I thought that
bears masturbated all winter.

—Damon R. Milhem

6. Of course, this discussion could cause Peter to post a clip of
Nat King Cole
(giess what his real surname is).

7. Of course, this discussion could cause Peter to post a clip of
Nat King Cole
(giess what his real surname is).

The first typo was my fault; the extra linebreaks in the second attempt
(tested again here) appear to be a new “feature”.

8. telescoper Says:

The noun “cole” can be found in English dictionaries as a generic name for plants of the cabbage family. It is related to the German kohl and scottish kail or kale. These are all derived from the latin word colis (or caulis) meaning a stem, which is also the root of the word cauliflower.

The surname “Cole” and the variant “Coles” are fairly common in England and Wales, but are not related to the latin word for cabbage. Both are diminutives of the name “Nicholas”.

9. […] I posted a little piece about Bayesian probability. That one and the others that followed it (here and here) proved to be surprisingly popular so I’ve been planning to add a few more posts […]

10. It already has a popular name: Stigler’s law of eponymy.

```
#### AMPS
```
Problema: Given the equation $7 x^2+6 x+9 y^2-5 y-8=0$, complete the square.

Passo a passo: Step 1:
\begin{array}{l}
 
\begin{array}{l}
 \text{Complete the square}: \\
 9 y^2-5 y+7 x^2+6 x-8=0 \\
\end{array}
Step 2:
\begin{array}{l}
 \text{Add }8 \text{to }\text{both }\text{sides}: \\
 9 y^2-5 y+7 x^2+6 x=8 \\
\end{array}
Step 3:
\begin{array}{l}
 \text{Group }\text{terms }\text{with }x \text{and }y \text{separately, }\text{leaving }\text{placeholder }\text{constants}: \\ \left(7 x^2+6 x+\underline{\text{   }}\right)+\left(9 y^2-5 y+\underline{\text{   }}\right)=\underline{\text{   }}+8 \\
\end{array}
Step 4:
\begin{array}{l}
 \left(7 x^2+6 x+\underline{\text{   }}\right)=7 \left(x^2+\frac{6 x}{7}+\underline{\text{   }}\right): \\
 \fbox{$7 \left(x^2+\frac{6 x}{7}+\underline{\text{   }}\right)$}+\left(9 y^2-5 y+\underline{\text{   }}\right)=\underline{\text{   }}+8 \\
\end{array}
Step 5:
\begin{array}{l}
 \left(9 y^2-5 y+\underline{\text{   }}\right)=9 \left(y^2-\frac{5 y}{9}+\underline{\text{   }}\right): \\
 7 \left(x^2+\frac{6 x}{7}+\underline{\text{   }}\right)+\fbox{$9 \left(y^2-\frac{5 y}{9}+\underline{\text{   }}\right)$}=\underline{\text{   }}+8 \\
\end{array}
Step 6:
\begin{array}{l}
 
\begin{array}{l}
 \text{Take }\text{one }\text{half }\text{of }\text{the }\text{coefficient }\text{of }x \text{and }\text{square }\text{it. }\text{Then }\text{add }\text{it }\text{to }\text{both }\text{sides }\text{of }\text{the }\text{equation, }\text{multiplying }\text{by }\text{the }\text{factored }\text{constant }7 \text{on }\text{the }\text{right.} \\
 \text{Insert }\left(\frac{\frac{6}{7}}{2}\right)^2=\frac{9}{49} \text{on }\text{the }\text{left }\text{and }7\times \frac{9}{49}=\frac{9}{7} \text{on }\text{the }\text{right}: \\
\end{array}
Step 7:
\begin{array}{l}
 8+\frac{9}{7}=\frac{65}{7}: \\
 7 \left(x^2+\frac{6 x}{7}+\frac{9}{49}\right)+9 \left(y^2-\frac{5 y}{9}+\underline{\text{   }}\right)=\fbox{$\frac{65}{7}$} \\\end{array}
Step 8:
\begin{array}{l}
 
\begin{array}{l}
 \text{Take }\text{one }\text{half }\text{of }\text{the }\text{coefficient }\text{of }y \text{and }\text{square }\text{it. }\text{Then }\text{add }\text{it }\text{to }\text{both }\text{sides }\text{of }\text{the }\text{equation, }\text{multiplying }\text{by }\text{the }\text{factored }\text{constant }9 \text{on }\text{the }\text{right.} \\
 \text{Insert }\left(\frac{\frac{-5}{9}}{2}\right)^2=\frac{25}{324} \text{on }\text{the }\text{left }\text{and }9\times \frac{25}{324}=\frac{25}{36} \text{on }\text{the }\text{right}: \\
\end{array}
Step 9:
\begin{array}{l}
 \frac{65}{7}+\frac{25}{36}=\frac{2515}{252}: \\
 7 \left(x^2+\frac{6 x}{7}+\frac{9}{49}\right)+9 \left(y^2-\frac{5 y}{9}+\frac{25}{324}\right)=\fbox{$\frac{2515}{252}$} \\
\end{array}
Step 10:
\begin{array}{l}
 x^2+\frac{6 x}{7}+\frac{9}{49}=\left(x+\frac{3}{7}\right)^2: \\
 7 \fbox{$\left(x+\frac{3}{7}\right)^2$}+9 \left(y^2-\frac{5 y}{9}+\frac{25}{324}\right)=\frac{2515}{252} \\
\end{array}
Step 11:
\begin{array}{l}
 y^2-\frac{5 y}{9}+\frac{25}{324}=\left(y-\frac{5}{18}\right)^2: \\
 \fbox{$
\begin{array}{ll}
 \text{Answer:} &  \\
 \text{} & 7 \left(x+\frac{3}{7}\right)^2+9 \fbox{$\left(y-\frac{5}{18}\right)^2$}=\frac{2515}{252} \\
\end{array}

{'problem': 'Given the equation $7 x^2+6 x+9 y^2-5 y-8=0$, complete the square.', 'step_by_step': 'Step 1:\n\\begin{array}{l}\n \n\\begin{array}{l}\n \\text{Complete the square}: \\\\\n 9 y^2-5 y+7 x^2+6 x-8=0 \\\\\n\\end{array}\nStep 2:\n\\begin{array}{l}\n \\text{Add }8 \\text{to }\\text{both }\\text{sides}: \\\\\n 9 y^2-5 y+7 x^2+6 x=8 \\\\\n\\end{array}\nStep 3:\n\\begin{array}{l}\n \\text{Group }\\text{terms }\\text{with }x \\text{and }y \\text{separately, }\\text{leaving }\\text{placeholder }\\text{constants}: \\\\\n \\left(7 x^2+6 x+\\underline{\\text{   }}\\right)+\\left(9 y^2-5 y+\\underline{\\text{   }}\\right)=\\underline{\\text{   }}+8 \\\\\n\\end{array}\nStep 4:\n\\begin{array}{l}\n \\left(7 x^2+6 x+\\underline{\\text{   }}\\right)=7 \\left(x^2+\\frac{6 x}{7}+\\underline{\\text{   }}\\right): \\\\\n \\fbox{$7 \\left(x^2+\\frac{6 x}{7}+\\underline{\\text{   }}\\right)$}+\\left(9 y^2-5 y+\\underline{\\text{   }}\\right)=\\underline{\\text{   }}+8 \\\\\n\\end{array}\nStep 5:\n\\begin{array}{l}\n \\left(9 y^2-5 y+\\underline{\\text{   }}\\right)=9 \\left(y^2-\\frac{5 y}{9}+\\underline{\\text{   }}\\right): \\\\\n 7 \\left(x^2+\\frac{6 x}{7}+\\underline{\\text{   }}\\right)+\\fbox{$9 \\left(y^2-\\frac{5 y}{9}+\\underline{\\text{   }}\\right)$}=\\underline{\\text{   }}+8 \\\\\n\\end{array}\nStep 6:\n\\begin{array}{l}\n \n\\begin{array}{l}\n \\text{Take }\\text{one }\\text{half }\\text{of }\\text{the }\\text{coefficient }\\text{of }x \\text{and }\\text{square }\\text{it. }\\text{Then }\\text{add }\\text{it }\\text{to }\\text{both }\\text{sides }\\text{of }\\text{the }\\text{equation, }\\text{multiplying }\\text{by }\\text{the }\\text{factored }\\text{constant }7 \\text{on }\\text{the }\\text{right.} \\\\\n \\text{Insert }\\left(\\frac{\\frac{6}{7}}{2}\\right)^2=\\frac{9}{49} \\text{on }\\text{the }\\text{left }\\text{and }7\\times \\frac{9}{49}=\\frac{9}{7} \\text{on }\\text{the }\\text{right}: \\\\\n\\end{array}\nStep 7:\n\\begin{array}{l}\n 8+\\frac{9}{7}=\\frac{65}{7}: \\\\\n 7 \\left(x^2+\\frac{6 x}{7}+\\frac{9}{49}\\right)+9 \\left(y^2-\\frac{5 y}{9}+\\underline{\\text{   }}\\right)=\\fbox{$\\frac{65}{7}$} \\\\\n\\end{array}\nStep 8:\n\\begin{array}{l}\n \n\\begin{array}{l}\n \\text{Take }\\text{one }\\text{half }\\text{of }\\text{the }\\text{coefficient }\\text{of }y \\text{and }\\text{square }\\text{it. }\\text{Then }\\text{add }\\text{it }\\text{to }\\text{both }\\text{sides }\\text{of }\\text{the }\\text{equation, }\\text{multiplying }\\text{by }\\text{the }\\text{factored }\\text{constant }9 \\text{on }\\text{the }\\text{right.} \\\\\n \\text{Insert }\\left(\\frac{\\frac{-5}{9}}{2}\\right)^2=\\frac{25}{324} \\text{on }\\text{the }\\text{left }\\text{and }9\\times \\frac{25}{324}=\\frac{25}{36} \\text{on }\\text{the }\\text{right}: \\\\\n\\end{array}\nStep 9:\n\\begin{array}{l}\n \\frac{65}{7}+\\frac{25}{36}=\\frac{2515}{252}: \\\\\n 7 \\left(x^2+\\frac{6 x}{7}+\\frac{9}{49}\\right)+9 \\left(y^2-\\frac{5 y}{9}+\\frac{25}{324}\\right)=\\fbox{$\\frac{2515}{252}$} \\\\\n\\end{array}\nStep 10:\n\\begin{array}{l}\n x^2+\\frac{6 x}{7}+\\frac{9}{49}=\\left(x+\\frac{3}{7}\\right)^2: \\\\\n 7 \\fbox{$\\left(x+\\frac{3}{7}\\right)^2$}+9 \\left(y^2-\\frac{5 y}{9}+\\frac{25}{324}\\right)=\\frac{2515}{252} \\\\\n\\end{array}\nStep 11:\n\\begin{array}{l}\n y^2-\\frac{5 y}{9}+\\frac{25}{324}=\\left(y-\\frac{5}{18}\\right)^2: \\\\\n \\fbox{$\n\\begin{array}{ll}\n \\text{Answer:} &  \\\\\n \\text{} & 7 \\left(x+\\frac{3}{7}\\right)^2+9 \\fbox{$\\left(y-\\frac{5}{18}\\right)^2$}=\\frac{2515}{252} \\\\\n\\end{array}\n'}

```
#### GSM8K
```
Problema: Natalia sold clips to 48 of her friends in April, and then she sold half as many clips in May. How many clips did Natalia sell altogether in April and May?

Resposta: Natalia sold 48/2 = <<48/2=24>>24 clips in May.
Natalia sold 48+24 = <<48+24=72>>72 clips altogether in April and May.
#### 72

{'question': 'Natalia sold clips to 48 of her friends in April, and then she sold half as many clips in May. How many clips did Natalia sell altogether in April and May?', 'answer': 'Natalia sold 48/2 = <<48/2=24>>24 clips in May.\nNatalia sold 48+24 = <<48+24=72>>72 clips altogether in April and May.\n#### 72'}

```
#### Mathlib4

```
Teorema: infinite_of_charZero (R A : Type*) [CommRing R] [Ring A] [Algebra R A]
    [CharZero A] : { x : A | IsAlgebraic R x }.Infinite
Prova: by
  letI := MulActionWithZero.nontrivial R A
  exact infinite_of_injective_forall_mem Nat.cast_injective isAlgebraic_nat
...

```
#### Coq Standard Library

```
Teorema: le_n_0_eq_stt
Prova: := fun n Hle => eq_sym (proj1 (Nat.le_0_r n) Hle).

```
