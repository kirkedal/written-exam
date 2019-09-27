# Written Exam LaTeX Package

This document describes the written-exam.sty latex package that is intended to be an easy way of setting up short written exams with space for inline answers.

The package now have initial support for answers. If answers are to be shown, use include with `\usepackage[solutions]{written-exam}`. If `solutions` property is omitted, solutions will not be shown.

## Document setup
The following command can be used to define the section title and weight of a question.

```latex
\questionhead{Section title}{Time/Weight}
```

The weight is only shown in the head, while the name is used later for the question name with the `\thequestion` command.


## True/False questions
True/false questions are setup in a table using the `tfquestion` environment. Each question is made using the `\tfitem[true|false]{question}` command.

```latex
\begin{tfquestion}
  \tfitem[true]{True/False statement 1}
  \tfitem[false]{True/False statement 2}
\end{tfquestion}
```

## Multiple-choice questions
Multiple-choice questions are made using the `mcquestion` environment. The question written inside the environment while each option is made using the `\mcitem[check|]{text}` command.

```
\begin{mcquestion}
  It this a good question?
  \mcitem[check]{Yes!}
  \mcitem{No!}
\end{mcquestion}
```

## Text answer questions
Text/exercise questions are made using the `question` environment. The question is written as normal text followed by some answer setup as defined below.

```
\begin{question}
  It this a question?

  [Answer setup, see below]
\end{question}
```
The environment is wrapped in a `samepage` environment to ensure that questions are not divided in two pages.


### Answer setup
Answers for students have the following options.

#### Lines
The basic command is `\answerline` that give a single line with room for text. 

```
\answerline
```

This is extended with the `\answerlines` command that given a number, makes this number of lines.

```
\answerlines{Number}
```
A further extension to this is `\answerlinesfill` that makes a number of lines such that rest of the page is filled. It enforces a `\newpage`.

```
\answerlinesfill
```

The color of a line is defined by the `rulecolor` coloe. It is as standard set to be gray:

```
\definecolor{rulecolor}{RGB}{127,127,127}
```

The height of each answer line is defined by the `\answerlineheight` length. It is as standard set to be 8 mm:

```
\setlength{\answerlineheight}{8mm}
```

#### Figure
Figure space is page width frameboxes defined by the `\answerfigure` command. It can be used in two ways:

You can define a figure box with a specific height by giving it a length argument:

```
\answerfigure{length}
```

If no argument is given it will make a figure box that fill the rest of the page:

```
\answerfigure
```

At the bottom of the box it is possible to make some text defined by the `\questionfiguretext` command. As standard it is defined to be:

```
\newcommand{\questionfiguretext}{\centering \small (figure space)}
```
Renew this command if you want another text.

### Short-hands

There a short-hand for making short answer questions with 5 answer lines using the `\shortquestion` command.

```
\shortquestion{Question text}
```

There is also a short-hand environment `longquestion` that works like `question`, but with a \answerlinesfill in the end.


## Solutions

[]
All solutions are defined to have `solutioncolor` which is currently green.

* You can show solution by changing `\usepackage{../written-exam}` to `\usepackage[solution]{../written-exam}`

You add solutions to true/false by
* `\tfitem[true]{text}`
* `\tfitem[false]{text}`

You add to mpc questions by
* `\mcitem[check]{text}`

You can add solutions to answerlines by
* `\answerlines[Text solution]{N}`
* `\answerlinesfill[Text solution]`

You can add general solutions (e.g. to tables) using
* `\ifsolution{text}`
There text will only be shown if text is set.

I will make it possible to have solutions for figures soon. But I might have to change it to an environment (edited)

I also made a `\ifsolutionelse{solution text}{text}` that can change a text

## Credits

Michael Kirkedal Thomsen, DIKU 2017.