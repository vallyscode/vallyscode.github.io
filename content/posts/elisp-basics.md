+++
author = "Valerii Lysenko"
title = "Intro to Emacs lisp"
date = "2019-09-19"
description = "Intro to emacs lisp."
tags = ["elisp"]
draft=false
+++

A basic overview of elisp to start crafting plugins and customizing Emacs. For more details see [docs](https://www.gnu.org/software/emacs/manual/html_node/elisp/index.html)

## Comments
Semicolon **;;** defines comment enywhere in a line

{{< highlight elisp "linenos=table,hl_lines=8 15-17,linenostart=0" >}}
;; Some text as comment
{{< / highlight >}}

## Arithmetic

{{< highlight elisp "linenos=table,hl_lines=8 4-5,linenostart=0" >}}
(+ 3 2 1) ;; 6
(- 8 5) ;; 3
(* 3 4) ;; 12
(/ 1 2.0) ;; 0.5
(/ 1 2) ;; 0
(% 12 5) ;; 2
(expt 3 4) ;; 81
{{< / highlight >}}

## Type conversions

{{< highlight elisp "linenos=table,linenostart=0" >}}
(float 6) ;; 6.0
(truncate 6.3) ;; 6
(floor 6.3) ;; 6
(ceiling 6.3) ;; 7
(round 6.3) ;; 6
(string-to-number "2") ;; 2
(number-to-string 2) ;; "2"
(char-to-string #xe0b0) ;; ""
{{< / highlight >}}

## Variables

### Global

{{< highlight elisp "linenos=table,linenostart=0" >}}
(setq x 1)
(setq a 3 b 2 c 7)
{{< / highlight >}}

### Local

{{< highlight elisp "linenos=table,linenostart=0" >}}
(let (a b)
 (setq a 3)
 (setq b 4)
 (+ a b))
{{< / highlight >}}

### Buffer-local

{{< highlight elisp "linenos=table,linenostart=0" >}}
 (setq-local x "some value")
{{< / highlight >}}

## Constants

{{< highlight elisp "linenos=table,linenostart=0" >}}
(defconst a "some value"
  "Some documentation.")
{{< / highlight >}}

## Functions

{{< highlight elisp "linenos=table,linenostart=0" >}}
{{< / highlight >}}

## Lambdas

{{< highlight elisp "linenos=table,linenostart=0" >}}
{{< / highlight >}}

## Control structures

### Sequencing

Evaluates all of the forms, in textual order, returning the result of the final form.

{{< highlight elisp "linenos=table,linenostart=0" >}}
 (progn a b c ...)
{{< / highlight >}}

Example:

{{< highlight elisp "linenos=table,linenostart=0" >}}
(progn (print "The first form")
       (print "The second form")
       (print "The third form"))
    -| "The first form"
    -| "The second form"
    -| "The third form"
  ⇒ "The third form"
{{< / highlight >}}

### Conditionals

If condition has the value nil, and no else-forms are given, **if** returns nil.

{{< highlight elisp "linenos=table,linenostart=0" >}}
(if nil
    (message "true")
  (message "false"))
⇒ "false""
{{< / highlight >}}

Variant of **if** where there are no else-forms, and possibly several then-forms.

{{< highlight elisp "linenos=table,linenostart=0" >}}
(when condition a b c)
{{< / highlight >}}

Same as can be represented using **if** expression

{{< highlight elisp "linenos=table,linenostart=0" >}}
(if condition (progn a b c) nil)
{{< / highlight >}}

Variant of **if** where there is no then-form

{{< highlight elisp "linenos=table,linenostart=0" >}}
(unless condition a b c)
{{< / highlight >}}


Same as can be represented using **if** expression

{{< highlight elisp "linenos=table,linenostart=0" >}}
(if condition nil (progn a b c))
{{< / highlight >}}

Conditional selects matching expressions

{{< highlight elisp "linenos=table,linenostart=0" >}}
(setq a 5)
(cond ((eq a 'hack) 'foo)
       (t "default"))
 ⇒ "default"
{{< / highlight >}}

### Combining conditions

**not** special form returns t if condition is nil, and nil otherwise.

{{< highlight elisp "linenos=table,linenostart=0" >}}
(not nil)
⇒ t
{{< / highlight >}}

**and** special form tests whether all the conditions are true.

{{< highlight elisp "linenos=table,linenostart=0" >}}
(and arg1 arg2 arg3)
{{< / highlight >}}

**or** special form tests whether at least one of the conditions is true.

{{< highlight elisp "linenos=table,linenostart=0" >}}
(or arg1 arg2 arg3)
{{< / highlight >}}

### Pattern-Matching

{{< highlight elisp "linenos=table,linenostart=0" >}}
(pcase (get-return-code x)
       ;; string
       ((and (pred stringp) msg)
        (message "%s" msg))
       ;; symbol
       ('success       (message "Done!"))
       ('would-block   (message "Sorry, can't do it now"))
       ('read-only     (message "The shmliblick is read-only"))
       ('access-denied (message "You do not have the needed rights"))
       ;; default
       (code           (message "Unknown return code %S" code)))
{{< / highlight >}}

### Iteration

**while** first evaluates condition. If the result is non-nil, it evaluates forms in textual order then it reevaluates condition, and if the result is non-nil, it evaluates forms again.

{{< highlight elisp "linenos=table,linenostart=0" >}}
(setq num 0)
      ⇒ 0
(while (< num 4)
  (princ (format "Iteration %d." num))
  (setq num (1+ num)))
      -| Iteration 0.
      -| Iteration 1.
      -| Iteration 2.
      -| Iteration 3.
      ⇒ nil
{{< / highlight >}}

Repeat-until loop, which will execute something on each iteration and then do the end-test

{{< highlight elisp "linenos=table,linenostart=0" >}}
(while (progn
        (forward-line 1)
        (not (looking-at "^$")))
    (do-something))
{{< / highlight >}}

Executes body once for each element of list, binding the variable var locally to hold the current element.

{{< highlight elisp "linenos=table,linenostart=0" >}}
(dolist (elt list)
            (setq value (cons elt value)))
{{< / highlight >}}

Executes body once for each integer from 0 (inclusive) to count (exclusive), binding the variable var to the integer for the current iteration.

{{< highlight elisp "linenos=table,linenostart=0" >}}
(dotimes (i 100)
          (insert (format "i: %s" i)))
{{< / highlight >}}



{{< highlight elisp "linenos=table,linenostart=0" >}}
{{< / highlight >}}


{{< highlight elisp "linenos=table,hl_lines=8 15-17,linenostart=199" >}}
(let ((x 1)
      (y 2)
      (z 3))
  ....)
{{< / highlight >}}
