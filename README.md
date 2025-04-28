# cs550-lab-3--resolution-for-first-order-logic-solved
**TO GET THIS SOLUTION VISIT:** [CS550 Lab 3- Resolution for First Order Logic Solved](https://www.ankitcodinghub.com/product/cs550-lab-3-resolution-for-first-order-logic-solved/)


---

📩 **If you need this solution or have special requests:** **Email:** ankitcoding@gmail.com  
📱 **WhatsApp:** +1 419 877 7882  
📄 **Get a quote instantly using this form:** [Ask Homework Questions](https://www.ankitcodinghub.com/services/ask-homework-questions/)

*We deliver fast, professional, and affordable academic help.*

---

<h2>Description</h2>



<div class="kk-star-ratings kksr-auto kksr-align-center kksr-valign-top" data-payload="{&quot;align&quot;:&quot;center&quot;,&quot;id&quot;:&quot;118169&quot;,&quot;slug&quot;:&quot;default&quot;,&quot;valign&quot;:&quot;top&quot;,&quot;ignore&quot;:&quot;&quot;,&quot;reference&quot;:&quot;auto&quot;,&quot;class&quot;:&quot;&quot;,&quot;count&quot;:&quot;2&quot;,&quot;legendonly&quot;:&quot;&quot;,&quot;readonly&quot;:&quot;&quot;,&quot;score&quot;:&quot;5&quot;,&quot;starsonly&quot;:&quot;&quot;,&quot;best&quot;:&quot;5&quot;,&quot;gap&quot;:&quot;4&quot;,&quot;greet&quot;:&quot;Rate this product&quot;,&quot;legend&quot;:&quot;5\/5 - (2 votes)&quot;,&quot;size&quot;:&quot;24&quot;,&quot;title&quot;:&quot;CS550 Lab 3- Resolution for First Order Logic Solved&quot;,&quot;width&quot;:&quot;138&quot;,&quot;_legend&quot;:&quot;{score}\/{best} - ({count} {votes})&quot;,&quot;font_factor&quot;:&quot;1.25&quot;}">

<div class="kksr-stars">

<div class="kksr-stars-inactive">
            <div class="kksr-star" data-star="1" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="2" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="3" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="4" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="5" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>

<div class="kksr-stars-active" style="width: 138px;">
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>
</div>


<div class="kksr-legend" style="font-size: 19.2px;">
            5/5 - (2 votes)    </div>
    </div>
Lab

Prelude

The format of this lab is a bit different from the previous ones: you won’t have to prove properties of a program using stainless. Instead, you will implement a resolution proof checker in scala. We still require that your implementation is accepted by stainless; this will ensure that some basic properties hold, and that all your functions terminate.

The implementation is split across multiple files, but you will only need to change Resolution.scala. We will explain the content of the other files as they become relevant.

For this lab, we provide you with some tests for your code. Use “`bash scala-cli test . “` to run them. We only provide you with some basic tests; as such, we strongly encourage you to add new tests.

We recommend that you frequently check that your implementation is accepted by stainless. You can use “`bash

Remember to add –solvers=smt-z3 if on MacOS

stainless src/*.scala –functions=

E.g.

stainless src/*.scala –functions=negationNormalForm,skolemizationNegation “ to only check a handful of functions. The–watch,–timeout=and–compact` flags might also prove useful.

Part one: Transforming formulas

The first thing to do is to put formulas in a form suitable for clausal resolution.

Have a look at Formulas.scala to see how identifiers, terms and formulas are described. You can ignore everything after (and including) Literal for now. It also defines some operations and predicates on them (e.g. substitute, freeVariables, containsNoExistential) which will be useful.

The transformation is done using 5 successive equivalence preserving transformations. You must have seen these in class, so we won’t describe them in details; please refer to the lectures for complete descriptions. – makeVariableNamesUnique is already implemented. It renames all variables so that each one is defined only once. You can see its behavior on some examples in Test.scala. – negationNormalForm pushes the negation operators as far down the tree as possible. – skolemizationNegation replaces all existential quantifiers with a skolem function. Note that having the formula in negation normal form and without name repetitions greatly simplifies its implementation. As such, its first step will be to apply the previous transformations. – prenexSkolemizationNegation pulls all quantifiers to the top of the formula. Once again, this is greatly simplified by the absence of existential quantifiers. This also means that all the quantifiers at the top will be universal quantifiers and can be left implicit; as such, this function should only return the matrix of the formula. – conjunctionPrenexSkolemizationNegation puts the formula in conjunctive normal form (CNF). Note that from that point on, formulas are represented using List[List[Literal]], so you should have a look at the remainder of Formulas.scala.

Part two: Proof checking

Once a formula is in conjunctive normal form (i.e. a List[List[Literal]]), one can use it to do proofs using resolution. As you’ve seen in class, a resolution proof is a list of clauses, each one being either part of the original formula (Assumed) or deduced from two previous clauses and a specific substitution (Deduced). Implement the function checkResolutionProof which, given a resolution proof, verifies that it is valid.

The system you’ve just implemented is not quite automated yet, but isn’t so far from it either. A practical implementation would also include a unification algorithm that would automatically compute the adequate substitution at each step. Then, a simple proof search procedure could try to unify all pairs of clauses, exploring the whole proof space.

If the initial formula was unsat, this procedure would end up producing the empty clause at some point. Hence this theorem-proving technique is refutationally complete.

Part three: The Dreadsbury Mansion Mystery

It is now time to use our proof checker!

We will use it to get to the bottom of the following mystery:

Someone who lives in Dreadbury Mansion killed Aunt Agatha. Agatha, the butler, and Charles live in Dreadbury Mansion, and are the only people who live therein. A killer always hates his victim, and is never richer than his victim. Charles hates no one that Aunt Agatha hates. Agatha hates everyone except the butler. The butler hates everyone not richer than Aunt Agatha. The butler hates everyone Aunt Agatha hates. No one hates everyone. Agatha is not the butler.

Stated more formally:

math egin{align} &amp; exists x. lives(x) land killed(x,a) \ &amp; lives(a) land lives(b) land lives(c) land

orall x. lives(x) ightarrow (x=a lor x=b lor x=c) \ &amp; orall x. orall y. killed(x,y) ightarrow (hates(x,y) land eg richer(x,y)) \ &amp; orall x. hates(a,x) ightarrow eg hates(c,x) \ &amp; orall x. hates(a,x) leftrightarrow x ot= b \ &amp; orall x. eg richer(x,a) leftrightarrow hates(b,x) \ &amp; orall

x. hates(a,x) ightarrow hates(b,x) \ &amp; eg exists x. orall y. hates(x,y) \ &amp; a ot= b end{align}

We implemented this in Mansion.scala. We also added some additional assumptions, such as commutativity of equality and Leibniz’s property for all predicates.

The transformation you implemented are then applied to all of these, resulting in the following assumed clauses:

Clauses

It introduces two skolem functions $0() which represents the killer, and $11(x) which given x, returns someone x doesn’t hate. We defined killer and notHatedBy to allow you to use these more easily.

As an example, one can then show that the killer is among Agatha, Butler and Charles by unifying assumptions 0 and 5 using the assignment $1 |&gt; $0().

Your first task is to prove that Charles is innocent. To do so, run “`shell

scala-cli run –watch . — 1 “ You should then completecharlesInnocentwith some steps (&lt; 5) to prove his innocence. The–watch` flag makes it so that your file will be re-compiled and run every time you do a change (and save). This will allow you to solve this interactively: run to see the initial assumptions, add a proof step, save (which triggers a re-run), see if your step is accepted by the checker, change it, save, add a new step, …; rinse and repeat until you proved Charles’ innocence.

Finally, you should prove that Agatha is the culprit. This require many steps; we did most of the reasoning for you, you should just add the few (&lt; 5) final steps, using the same workflow as for the for the first proof fragment. Use this command: “`shell scala-cli run –watch . — 2 “`

Submission

Once you have implemented, you can submit your Resolution.scala file on Moodle.

You are not allowed to change the signature of any function. If you add helper functions, they should be in Resolution.scala.

Only one member of each group should submit a solution.
