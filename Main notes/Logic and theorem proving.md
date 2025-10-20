**Tags:** [[Maths]]

# Natural deduction proofs

Which is the idea of searching through a set of inference rules to prove something

Proof by induction:
- Assume P(0) true
- Prove that if P(n) true, P(n+1) true (implication)

Proof by structural induction:
- Same concept but generalized to act on formulas
- Assume that P(a) true for every atomic formula P(a)
- Prove that P(A) holds for a composite formula composed of atomic formulas for which P(a) holds

In recursive functions that act on formulae structures, we use different cases for every possible atomic formula and recursively reduce the formula that is evaluated (while keeping the previous result somewhere if needed) based on those possible cases
eg. (not (p and q)) or (p or s)
- The first evaluated subformula is (a or b):
a=(not (p and q))
b=(p or s)
which is an atomic formula using the "or" operator
- The second evaluated formula is (not x):
x=(p and q)
which is an atomic formula using the "not" operator
- And so on, with making sure to go back to any unevaluated subformulas resulting from a formula that is composed of 2 formulas

The truth value of a formula in an assigbment can be computed with a simple recursive algorithm:
- The input variables would be 1 and 0 respectively depending in the truth value of the variable
- Logical operators would be mathematical operators(eg. not returns 0, and returns p×q, or returns p+q) to get a final result of either 1 or 0 indicating the truth value

Satisfaction: an assignement x satisfies a formula (or proposition) p if the truth value of p(x)=1
A formula p is said satisfiable if, by definition, there exists at least one assignment x for which p holds true
A formula that is not satisfiable is called a contradiction
valid formula = tautology
Contingent formula : neither a contradiction nor a tautology
Semantical consequence: say we have a set of formula, if there exists an assignment for which all the formulas from that set hold true, and that assignment is also a model of ( = for which a given formula holds) a formula p, then p is a semantical (or logical/tautological) consequence of that set. Denoted by "|=".

A set is consistent if (((x1 and x2) and ...) and xn) is satisfiable, and inconsistent if it is not
Basically: (((ϕ1 ∧ ϕ2) ∧ . . .) ∧ ϕn) →ϕ 

Sequent = Syntactical consequence = if given a set of premises (x1..xn), y is true, then {x1..xn} |- is a Sequent
eg. {p,q} |- (p and q)

An inference rule is composed of:
- A set of sequents called the hypotheses of the rule
- A sequent called the conclusion of the rule
- A possible condition for applying the rule
- A name

Inference rules that have 0 hypotheses are called axioms

A proof system is a set of inference rules

We can extend a set of premises of a valid rule and still get a valid rule, this is called the "extend" rule

Formal proof: using a set of proof rules and premises in a proof system to prove another rule

Derived proof rules are used to shorten other proofs (reduce/simplify the formula). A derived rule is a proof rule that we can prove using the other proof rules ina given proof system, through a formal proof.

Soundness: For any set of formulae Γ and any formula ϕ, if the sequent Γ |- ϕ is valid, then Γ |= ϕ is valid

Completeness: For any set of formulae Γ and any formula ϕ, if Γ |= ϕ then the sequent Γ |- ϕ is valid

# Proof by resolution

Resolution is a more practical deductive system for automated proofs as it allows more performant implementations in computation

A literal is a formula that can't have only one outcome, and the outcome is equal to the truth value of a proposition or its negation.
A clause is a disjunction of literals.
The empty clause is a clause with 0 literals and is unsatisfiable, denoted as a contradiction.

Conjunctive normal form (CNF) is when a formula is a conjunction of clauses.
Disjunctive normal form (DNF) is a disjunction of conjunction of literals.

Resolution is a system with only one inference rule. The conclusion and hypotheses are clauses.
A formal proof using resolution is a clause from a set of clauses which is a sequence of clauses for which a clause from that set is either (1) a clause from the original set of clauses or (2) found by resolution through clauses that satisfy the first condition.

Resolution is sound but not complete.

A formula is satisfiable if its CNF is satisfiable.

To establish a logical consequence by resolution:
- We know that x is a logical consequence of a set of clauses if the CNF of that set of clauses implies x. Therefore, we put the negation of the formula in CNF and prove that the outcome is the empty clause, which is a contradiction, meaning our initial clause (hypotheses) is valid.

A unification problem is a finite set of equations to solve. If the right side of each equation contains no free variables (meaning the term is closed) the problem is called pattern matching.
Higher order unification deals with variables that are functions, first order unification deals with the rest. If a solution is required to make both sides of an equation literally equal, then it's called syntactic unification, otherwise it's called semantic unification.

The resolution rule in propositional logic is a single valid inference rule that produces a new clause implied by two clauses containing complementary literals. Two literals are said to be complements if one is the negation of the other.

Proof by resolution (technique):
- All clauses in the knowledge base are concatenated with the negation of the clause that we wabt to prove in conjunctive form (by "and"ing them together). This is the basis of our refutation.
- This outputs a set of clauses. The resolution rule is then applied to all possible pairs of that set. If it does not derive the empty clause, meaning all clauses have been discarded, then the refutation holds and the proof doesn't. When the resolution rule is applied to two clauses with complementary literals (remember that a clause is a disjunction of literals), they are both discarded, otherwise they stay in the set awaiting another application of the rule with other clauses. If it does not derive the empty clause and there are no more possible pairs to apply the resolution rule to, that means the conjecture (clause we want to prove) is not a theorem of the knowledge base. Otherwise the proof is valid (ie. empty clause is derived).


