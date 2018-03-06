# Theory of Computing Midterm Review

- Regular Language:

  - Finite Automata: 

    - Definition: a 5-tuple $(Q,\Sigma,\delta,q_0,F)$ , $Q$ is a **finite** set of states, $\Sigma$ is a **finite** set of alphabet, $\delta$ is the transition function, $q_0 \in Q$ is the start state, $F \in Q$ is the set of accept states
    - Notation: $L(M) = A$ , $M$ **recognizes** $A$
    - Notes:
      - A machine only recognizes one language, and even if accepts no string, still recognizes the empty language $\emptyset$ ; 
      - The transition function specify exactly **one** next state for each possible combination of state and input symbol;
      - If a machine's start state is an accept state, $\varepsilon$ is accepted;

  - Computation:

    - The three conditions of $M$ accepts $w$

      1. $r_0 = q_0$,

      2.  $δ(r_i, w_{i+1}) = r_{i+1}, \text{for  } i = 0, . . . , n − 1$, and
      3.  $r_n ∈ F$.

    - Definition of Regular Language: if some finite automation recognizes it.

    - Prove a Regular Language: 

    - Design an Finite Automata:

  - Non-determinism:

    - In a **nondeterministic** machine, several choices	may exist for the next state at any point, it is a generalization of determinism; 
    - Different between **DFA** and **NFA**:
      1. In an NFA,  a state may have zero, one, or more exiting arrows for each alphabet symbol, but every state of DFA has exactly one;
      2. NFA may have zero, one, or more arrows labeled with members of the alphabet, or $\varepsilon$ 
    - NFA considers all possibilities and if any of the possibilities is in an accept state, the NFA accepts the string. 
    - Equivalence of **NFA** and **DFA**:
      - Two machines are equivalent if they recognize the same language
      - Theorem: Every nondeterministic finite automation has an equivalent deterministic finite automation
        - Proof:
          1. If **NFA** has $k$ stats, then the **DFA** has $2^k$ states;
          2. the start states of $DFA$ is the start states of **NFA** plus the states that can be reached by travelling along 0 or more $\varepsilon$ arrows, the accept states contain **NFA** 's all accept states;
          3. modify the transition function: goes to $\emptyset$ if no arrow exits, and goes to states containing the set can be obtained by following the $\varepsilon$ arrow;
          4. Removing states with no arrow points at them.
      - Theorem: A language is regular if and only if some **NFA** recognizes it:
        - Proof: 
          - if some NFA recognizes a language, so does some DFA
          - every regular language has some DFA recognizes it, and DFA is also an NFA

  - Regular Operations: 

    - Let $A$ and $B$ be languages, define the following operations:
      - **UNION** : $A \cup B = \{x|x \in A \text{or} x\in B\}$
      - **CONCATENATION**: $A \circ B = \{xy| x\in A \text{ and } y\in B\}$
      - **STAR**: $A^* = \{x_1x_2 \dots x_k | k \geq 0 \text{ and each } x_i \in A\}$
        - Note: the empty string $\varepsilon$ is always in the $A^*$ , no matter what $A$ is.
    - Theorems:
      - The class of regular language is closed under the union operation, that is, if $A_1$ and $A_2$ are regular languages, so is $A_1 \cup A_2$ 
        - Proof 1:  proof by construction, simulate a $M$ for $A_1 \cup A_2$ from $M_1$ and $M_2$; need to remember $k_1 \times k_2$ states, and the accept states are those pairs wherein either $M_1$ or $M_2$  is in an accept state; initial state is the pair $(q_1, q_2)$ 
        - Proof 2: proof with **NFA**, using $N$ to simulate $N_1$ and $N_2$; $N$ will have a new start state that branches out to the start states of $N_1$ and $N_2$ with $\varepsilon$ arrows
      - Closure under the concatenation operation
        - Proof: take an **NFA** $N$ to simulate $N_1$ and $N_2$, the start state of $N$ is the start states of $N_1$ ,and whenever at an accept state of $N_1$, link to $N_2$'s start state with $\varepsilon$ arrows. 
      - Closure under the start operation
        - Proof: whenever $N_1$ is at an accept state, return to the start state with $\varepsilon$ arrows.

  - Regular Expression:

    - The value of a regular expression is a language;
    - Formal Definition: this is an inductive definition, defining regular expression in terms of smaller regular expression and avoiding circularity
      1. $a$ for some $a$ in the alphabet $Σ$,
      2. $ε$,
      3. $∅$, Notes: $\varepsilon$ is the language containing one element - empty string, $\emptyset$ is the language containing no string
      4. $(R_1 ∪ R_2)$, where $R_1$ and $R_2$ are regular expressions,
      5. $(R_1 ◦ R_2)$, where $R_1$ and $R_2$ are regular expressions, or
      6. $(R^∗_1)$, where $R_1$ is a regular expression.
    - Generalized Nondeterministic Finite Automation:
      - **NFA** with transition arrows may have regular expression, **GNFA** reads block of input symbol, which themselves constitute a string described by the regular expression on that arrow
      - Converting **DFA** to **GNFA** under special conditions:
        1. the start state has transition arrows going to every other state but no arrows coming in from any other state
        2. one single accept state, arrows coming from every other states but no arrow going to any other state, not the same as start state
        3. except for the start and accept states, one arrow goes from every state to every other state and also from each state to itself;
           - The conversion can be done by simply adding a new start state with an $\varepsilon$ arrow to the old start state and a new accept state with $\varepsilon$ arrows from the old accept states, if any arrow has multiple labels, replace each with a single arrow whose label is the union of the previous labels; finally add arrows labeled $\emptyset$ between state that had no arrows; the conversion between the special form **GNFA** with $k$ states into a regular expression can be done by constructing an equivalent **GNFA** with $k-1$ states;
           - Constructing **GNFA** with one fewer state when k>2: rip out one state that is not the start or accept state, and repair the machine so that it still recognizes the language; 
             - the new arrow between $q_i$ and $q_j$ will compensate all the strings from $q_i$ to $q_j$ directly or via $q_{rip}$ 
    - Equivalence with Finite Automation:
      - Theorem: A language is regular if and only some regular expression describes it
        - if a language is described by some regular expression, then it is regular:
          - Proof: covert the expression $R$ describing $A$ to a $NFA$ recognizing $A$, only need to prove the $\varepsilon$ case where the start state is the accept state, and the empty string case where there is no accept state. 
        - if a language is regular, then some regular expression describes it:
          - Proof: converting some **DFA** recognizing $A$ into a regular expression $R$ describing it; proved by  **GNFA**, call the CONVERT(G) recursively, stop at $k=2$ where it can be converted to a regular expression, if $k>2$, select a $q_{rip}$ state and repair the machine; 

  -  Non-regular Languages: prove that certain languages cannot be recognized by any finite automation

    -  The pumping lemma for regular language:

      -  If A is a regular language, then there is a number p (the pumping length) where if s is any string in A of length at least $p$, then s may be divided into three pieces, $s = xyz$, satisfying the following conditions:

        1. for each$ i ≥ 0, xy^iz ∈ A$,
        2. $|y| > 0$, and
        3. $|xy| ≤ p$.

      -  As a pumping game: The Pumping Game for language L (between players R and N):      

         ​	Step 1:  R picks integer $p$, so that:  $p >= 0$.      

         ​	Step 2:  N picks string  $w$ in $L$, so that: $|w| >= p$.      

         ​	Step 3:  R picks strings $x y z$,  so that: $xyz=w, |xy| <= p, |y| > 0$.      

         ​	Step 4:  N picks integer $i >= 0$, so that: $x y^i z$ is NOT in $L$.    

         - The winner is the last player to make a valid move.  In particular    N wins if they can finish Step 4.
         - Theorem:
           - If $L$ is regular, then R has a winning strategy
           - If N has a winning strategy, then $L$ is irregular

      - Proof: Pigeonhole Principle, if $p$ pigeons are to be placed in to fewer than $p$ holes, some hole has to have more than one pigeon

        - Let $n$ be the pumping length $p$, then $n+1$ must be larger than $p$ the number of states, , so the sequence must contain some repeated state. 
        - TODO:

    - L-equivalent: string $x$ and $y$ are not L-equivalent, if there is some string $z$ so that exactly one $xz, yz$ is in $L$, $z$ is a distinguishing suffix for $x$ and $y$, find $S$ as an infinite set of strings, if no two distinct states in $S$ are L-equivalent, then $L$ will have at least $|S|$ states ($\infty$), which is not allowed for **finite** automata 

- Context-Free Languages:

  $REG$ is a proper subset of $CFL$ , and $CFL$ is a proper subset of $ALL$

  - Context-Free Grammars:

    - The following grammar:

      $A → 0A1$
      $A → B$
      $B → \#$

      Each rule appears as a line in the grammar, comprising a symbol and a string separated by an arrow. The symbol is called a variable. The string consists of variables and other symbols called terminals.

    - Formal Definition: A context-free grammar is a 4-tuple$ (V,Σ,R, S)$, where

      1. $V$ is a finite set called the variables,
      2. $Σ$ is a finite set, disjoint from V , called the terminals,
      3. $R$ is a finite set of rules, with each rule being a variable and a
        string of variables and terminals, and
      4. $S ∈ V$ is the start variable.

    -  Design a Context-free Grammar: TODO

    -  If a grammar generates the same string in several different ways, we say that the string is derived **ambiguously** in that grammar. If a grammar generates some string ambiguously, we say that the grammar is **ambiguous**. Some context-free languages, however, can be generated only by ambiguous grammars. Such languages are called **inherently ambiguous**.

    -  Chomsky Normal Form: A context-free grammar is in Chomsky normal form if every rule is of the form:

       ​		$A → BC$
       ​		$A → a$
       where a is any terminal and $A, B$, and $C$ are any variables—except that $B$ and $C$ may not be the start variable. In addition, we permit the rule $S → ε$, where $S$ is the start variable.

       - Theorem: Any context-free language is generated by a context-free grammar in Chomsky
         normal form.
         - Proof: Also way to convert to **CNF**, 
           - $S_0$ and the rule $S_0 → S$
           - $\varepsilon$ - rule,  remove $A → ε$, where A is not the start variable. Then for each occurrence of an A on the right-hand, add a new rule with that occurrence deleted: $R → uAv$, add $R → uv$; note: $R → uAvAw$ would turn to $R → uvAw| uAvw| uvw$ , $R → A$ turns to $ R → ε$.
           - unit-rule, remove  $A → B$. Then,whenever a rule $B → u$ appears, add the rule $A → u$ unless this was a unit rule previously removed.
           - convert all remaining rules into the proper form. We replace each rule $A → u_1u_2 · · · u_k$, where $ k ≥ 3$ and each $u_i$ is a variable or terminal symbol with rules so that terminals becomes variables
       - Parsing question: given $w$ and $G$, is $w$ in $L(G)$ 
         - CYK algorithm: 
           - convert G to **CNF**
           - put length 1 substring in the table
           - for each substring $w_i \dots w_j $ of $w$, if it can be separated to two substrings that are already in the table, place it in the table(i,j)
           - if $S$ is in table (1,n), accept
           - $O(N^3)$ 

  - Pushdown Automata: **NFA** with stack 

    - Formal Definition: A pushdown automaton is a 6-tuple $(Q,Σ, Γ, δ, q0, F)$, where $Q, Σ,Γ$ and $F$ are all finite sets, and

      1. $Q$ is the set of states,
      2. $Σ$ is the input alphabet,
      3. $Γ$ is the stack alphabet,
      4. $δ : Q × Σ_ε × Γ_ε−→P(Q × Γ_ε)$ is the transition function,
      5. $q_0 ∈ Q$ is the start state, and
      6. $F ⊆ Q$ is the set of accept states.

    -  “$a,b → c$” to signify that when the machine is reading an $a$ from the input, it may replace the symbol $b$ on the top of the stack with a $c$; This PDA is able to get the same effect by initially
       placing a special symbol \$ on the stack. Then if it ever sees the \$ again, it knows that the stack effectively is empty.

    -  Theorems: A language is context free if and only if some pushdown automaton recognizes it

       -  If a language is context free, then some pushdown automaton recognizes it.

          - Proof: design a **PDA** to determine whether some series of substitutions using the rules of the **CFG** $G$ will lead from the start variable to $w$ accepted by the **PDA**. Store part of the intermediate string starting with the first variables (the terminals are matched immediately) 

       -  If a pushdown automaton recognizes some language, then it is context free.

          -  Proof: $G$ should generate a string if that string causes the **PDA** to go from its start state to an accept state. 

             -  Three special conditions: 

                1. It has a single accept state, $q_{accept}$.
                2. It empties its stack before accepting.
                3. Each transition either pushes a symbol onto the stack (a push move) or pops
                  one off the stack (a pop move), but it does not do both at the same time: replace each transition that simultaneously pops and pushes with a two transition sequence that goes through a new state, and we replace each transition that neither pops nor pushes with a two transition sequence that pushes then pops an arbitrary stack symbol

             -  denote $(p,s)$ as configuration of **PDA** that it is at state $p$, with stack $s$, For each pair of states $p$ and $q$ in $P$, the grammar will have a variable $A_{pq}$ generates all strings that can also take P from p to q, regardless of the stack contents at p, leaving the stack at q in the same condition as it was at p.

             -  Three classes of rules:

               1. suppose $u$ is a stack variable, and one $(r,u)$ to push, one $(s,u)$ to pop, add rule: $A_{pq} \to aA_{rs}b$ , such rule capture computation from $(p,\varepsilon)$ to $(q,\varepsilon)$ , so symbol pushed on first step is not popped until the last step

               2. for any three stats $p,r,q$, add $A_{pq} \to A_{pr}A_{rq}$ , handle symbols pushed on first step popped before last step

               3. $A_{pp} \to \varepsilon$ handle 0 step

                  Choose start symbol $S = A_\text{init,final}$  

  - Non-context-free Languages

    - Pumping Lemma for **CFL**: If A is a context-free language, then there is a number p (the pumping length) where, if s is any string in A of length at least p, then $s$ may be divided into five pieces $s = uvxyz$ satisfying the conditions:

      1. for each $i ≥ 0, uv^ixy^iz ∈ A$,
      2. $|vy| > 0$, and
      3. $|vxy| ≤ p$.

    -  As a game: CONTEXT-FREE PUMPING GAME FOR L:

       Step 1. Player C picks an integer $p$, such that: $p >= 0$.

       Step 2. Player N picks a string $s$, such that: $s$ is in L, $|s| >= p$

       Step 3. Player C picks strings $u,v,x,y,z$, such that: $uvxyz=s, |vy| >= 1, |vxy| <= p$.

       Step 4. Player N picks an integer $i$, such that: $i >= 0, u v^i x y^i z$ is not in L.

       - Theorem: 
         - If L is context free, then C has a winning strategy.
         - If N has a winning strategy, then L is not context-free.
       - COROLLLARY: CFL's are NOT closed under intersection,  and not closed under complementation.
       - Practice: winning strategy: TODO

- The Church-Turing Thesis:

  - Turing Machine:

    - Summary:
      - A Turing machine can both write on the tape and read from it.
      - The read–write head can move both to the left and to the right.
      - The tape is infinite.
      - The special states for rejecting and accepting take effect immediately.
    - Formal Definition: A Turing machine is a 7-tuple,$ (Q,Σ, Γ, δ, q0, q_\text{accept}, q_\text{reject})$, where $Q, Σ, Γ$ are all finite sets and
      1. $Q$ is the set of states,
      2. $Σ$ is the input alphabet not containing the blank symbol $\sqcup$,
      3. $Γ$ is the tape alphabet, where $\sqcup ∈ Γ$ and $Σ ⊆ Γ$,
      4. $δ : Q × Γ−→Q × Γ×{L,R}$ is the transition function,
      5. $q_0 ∈ Q$ is the start state,
      6. $q_\text{accept} ∈ Q$ is the accept state, and
      7. $q_\text{reject} ∈ Q$ is the reject state, where $q_\text{reject} \neq q_{accept}$.
    - Note: $\Sigma$ doesn't contain the blank symbol $\sqcup$ ; The Turing Machine works as follow:
      1. The head starts on the leftmost square on the tape, marking the end of the input
      2. Computation proceeding according to the transition function, stay at the position if head movement would exceed the left limit of the tape.
      3. Enter the reject or accept position, otherwise run forever. 
    - Configuration: current state, the current tape contents, and the current head location, $u q v$, $uv$ is the current tape content, and the current head location is the first symbol of $v$. 
      - C1 yields  C2 if the Turing machine can legally go from C1 to C2 in a single step
    - Call a language Turing-recognizable if some Turing machine recognizes it.
      - Call a language Turing-decidable or simply decidable if some Turing machine decides it
        - deciders always make a decision to accept or reject
    - Examples of Turing Machine: TODO

  - Busy-beaver:  consists of designing a halting, binary-alphabet Turing machine which writes the most 1s on the tape

    - The busy-beaver function $\Sigma$ is a noncomputable function that quantifies the maximum score attainable by a Busy Beaver on a given measure;
    - if $f: ℕ → ℕ$ is any computable function, then$ Σ(n) >f (n)$ for all sufficiently large *n*, and hence that Σ is not a computable function.
      - This implies that there is no general algorithm to decide whether an arbitrary Turing Machine is a busy beaver 
    - $\Sigma(0) = 0, \Sigma(1) = 1, \Sigma(2) = 4 , \Sigma(3) = 6 ,  \Sigma(4) = 13, \Sigma(5)\geq 4098$

  -  Variant of Turing Machine:  for each variants, show that it is equivalent to Sipser's standard Turing Machine

    - Two-way infinite vs. One-way infinite

      - Filling two ways with empty symbols $\sqcup$ vs. only filling one way
      - Simulating one-way with two-way: add another special symbol to left of the input, if ever see the special symbol, step right. 
      - Simulating two-way with one-way: 
        - At start, add special symbol $\wedge$ to the left, and \$ to the right (indicating the end of the input string)
        - During simulation, if ever see \$, replace with $\sqcup$ \$ 
        - If ever seen $\wedge$, shift the entire string up to \$ one step to right, make room for $\sqcup$ 
        - After **T** steps on the input of length $N$ , tape has length $O(T+N)$, time complexity is $O(T \dot (T+N))$ , polynomial slow down

    - K-tape TM

      - Initially the input is on one tape, and the others are blank, the transition function allow for reading, writing and moving the heads on some or all of the tapes simultaneously
      - Use \# to keep track of different tapes, and a dot above to indicate heads, this means the one-tape TM has a larger alphabet as it will need to consider the dot
      - $O(n+T)$ to simulate one step, $O(T(N+T))$ overall, polynomial slow down

    - Determinism vs. Non-determinism

      - Both start with the same configuration, Determinism is a path, non-determinism is a tree

      - for a given **NTM** M, its tree has a maximum branching factor b, max number of arrows consistent with any one situation

      - Three possible outcome of **NTM** M , with a input $w$

        1. If there exists a path to $q_\text{accept}$ , then M accepts w;
        2. if every path ends without accepting, then reject
        3. if no path accepts, but some go on forever, then M runs forever.

        The challenge is to design deterministic TM, for a **NTM** so that it has the same outcome as the **NTM**

      - Use BFS:

        - exploring the computation tree of $M$ and $w$ level by level, if every find accept, ACCEPT, if the whole level has no further path, REJECT, else keep going
        - Use three tapes (according to k-tape , this is equivalent to a one tape), use the first to store the input, the second to simulate some branch, the third to store the address 
          1. Initially, tape 1 contains the input w, and tapes 2 and 3 are empty.
          2. Copy tape 1 to tape 2 and initialize the string on tape 3 to be ε.
          3. Use tape 2 to simulate N with input w on one branch of its nondeterministic
             computation. Before each step of N, consult the next symbol on tape 3
             to determine which choice to make among those allowed by N’s transition
             function. If no more symbols remain on tape 3 or if this nondeterministic
             choice is invalid, abort this branch by going to stage 4. Also go to stage 4
             if a rejecting configuration is encountered. If an accepting configuration is
             encountered, accept the input.
          4. Replace the string on tape 3 with the next string in the string ordering.
             Simulate the next branch of N’s computation by going to stage 2.
        - The slow down is exponential

    - Note: all variants agree on recognizable and decidable

  - Enumerator:  TM with a 'printer', we let it run forever, it prints out or enumerates some languages

    - Language $L$ is enumerable if some enumerator $E$ enumerates it
    - if $L$ is decidable, then it is enumerable (if some decider accept, E prints it)
    - L is recognizable iff L is enumerable
      - Decider doesn't work as some string may run forever
        - For an input, use a time limit $T$
        - Round-robin to run many strings at once: run a M for i step on each input $s_i$ from the list of all possible strings , if any computation accepts, print out $s_j$
          - If M accepts a particular string s, eventually it will appear on the list generated by E. In fact, it will appear on the list infinitely many times because M runs from the beginning on each string for each repetition of step 1. This procedure gives the effect of running M in parallel on all possible input strings.
      - $ E \to M$ , run $E$, every time it outputs a string, compare it with $w$, if $w$ appears, accept

  - Algorithm: 

    - Anything we can compute with a general computer can be computed by a TM
    - RAM: random access machine
      - CPU basic op: arithmetic operation, jump (to instruction), LOAD and STORE
        - Every time STORE $M[i]=j$: write $(i,j)$ on the memory tape
        - Every time want to LOAD $M[i]$, search for the last occurrence of $(i,$ and return the $j$ 
      - Program is a sequence of codes in memory
      - Given an RAM, it can be simulate by TM 
    - Church-Turing Thesis: TM is algorithms
      - If an algorithm always halt, then some corresponding decision problem is decidable.
      - ​

- Decidability:

  - Decidable Language:

    - Decidable problem concerning regular languages:
      - the acceptance problem for DFAs of testing whether a particular deterministic finite automaton accepts a given string can be expressed as a language, $A_\text{DFA}$: 
        - $A_\text{DFA} = \{⟨B,w⟩| \text{B is a DFA that accepts input string w}\}$
        - Theorems:
          -  $A_\text{DFA}$ is a decidable language: propose a TM that decides $A_\text{DFA}$ 
          - $A_\text{NFA}$ is a decidable language.
          - $A_\text{REX}$ is a decidable language.
      - emptiness testing for the language of a finite automaton, whether or not a finite automaton accepts any strings at all:
        - $E_\text{DFA} = \{⟨A⟩| \text{A is a DFA and L(A)} = ∅\}$
        - Theorems:
          - $E_\text{DFA}$ is a decidable language
          - $E_\text{QDFA} = \{⟨A,B⟩| \text{A and B are DFAs and L(A) = L(B)}\}.$
    - Decidable problem concerning context free languages:
      - $A_\text{CFG}$ is a decidable language
      - $E_\text{CFG}$ is a decidable language.
      - Every context-free language is decidable

  - Undecidability:

    - $\mathcal{R}$, real number, is uncountable. 
      - Proof: give a list of real numbers (arbitrary), construct a new real number that is not in the list by going through the diagonal of the table for $f$ and arbitrarily pick a different number

    ​