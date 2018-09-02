## On Variables and Substitution

(under construction)

### Abstract

Variables---and operations of substituting values for variables---play an important role in mathematics and computer science. Whenever we want to design programming languages or build tools such as compilers, a careful understanding of variables is necessary. The difficulties and subtleties that arise in a study of variables link up with two of the most beautiful mathematical theories that are currently under intense development, the theory of nominal sets and the theory of string diagrams, both of which are children of category theory. In this talk, I will give an overview of the area and briefly touch on some ongoing collaboration with Samuel Balco. 

I hope that the presentation would appeal in equal measure to students of mathematics and of computer science.

### Introduction

I try to make the talk interesting for students of maths and of computer science. 

I also want to show you some category theory, an important area of mathematics that is of fundamental importantce, but not even taught at all universities. One of many reason why category theory is important is that it links up mathematics and computer science, and we can also add logic and phsyics, even though that will not play a big role in this talk. 

So let us start with a dictionary.

mathematics| computer science | category theory | logic | physics
-----------|-------------|------------| ---- |--
set | data type | object | proposition | space
function | program | arrow | proof | transformation

I will illustrate the nature of this landscape with a research question on which I have done worked recently. But the emphasis is on giving an example for the power of the dictionary above.

### Preliminaries: Substitution, Free and Bound Variables

#### Substitution

...

#### Free and Bound Variables

The following definitions are not completely precise, but they can be made precise in all relevant circumstances known to me.

A ***fresh variable*** is a variable that has not been used before.

A ***bound variable*** is a variable that can be renamed by a ***fresh variable*** without changing its meaning.

**Example 1:** If we define a function, for example

    f(x) = x^2 + 2x + 1
    
then `x` is a bound variable. Indeed

    f(y) = y^2 + 2y + 1
    
defines the same function. To run through the definitions, `y` is *fresh* in `f(x) = x^2 + 2x + 1` since `y` does not occur in `f(x) = x^2 + 2x + 1`. And if we substitute `x` by `y`, then the meaning of the expression does not change.

**Example 2:** A programming example ... tba ... 

#### Substitution and Bound Variables

In the presence of bound variables, we need to be careful with substitution.

...

### The Research Question

A calculus of substitutions that ...

What is new? String diagrams ... enter category theory ...

### Preliminaries: Categories 

One of the many ways of looking at category theory is as a theory of compositionality. This is important to programming and software engineering as we need to build big systems from small systems we understand in a compositional way. "Compositional" here refers to being able to deduce properties of the big system from known properties of the smaller components.

Category theory has to say a lot about compositionality in many different ways.

To start with, a category is a mathematical structure that has "arrows" and composition of arrows.

**Def:** A category **A** consists of a set of objects, also denoted by **A**, and for any two objects A,B a set of arrows **A**(A,B). There are special arrows *id_A*, called identiy arrows or identities, for all A in **A** and for any *f* in **A**(A,B) and *g* in **A**(B,C) there is an arrow *f;g*, called the composition of *f* and *g*. This data is required to satisfy tha laws of identity and associativity.

To express that *f* is an element of **A**(A,B), we also write <a href="https://www.codecogs.com/eqnedit.php?latex=f:a\to&space;b" target="_blank"><img src="https://latex.codecogs.com/gif.latex?f:a\to&space;b" title="f:A\to B" /></a> and call A the domain or source of *f* and B the codomain or target. The composition *f;g* is also written as *gf*.

**Example:** 
- Let **Set** be the category that has sets as objects and all functions as arrows.
- Given a countably infinite set **N**, the category **Fin** ...
- The category **Card** consists of finite cardinals.

One should check that this is indeed a category. But we know that we can compose functions and that there is an idenity function.

This example is a bit boring, at least at first sight. So why is category theory interesting? 

- Going back to our dictionary, there are many categories that are very different from **Set**. 
   - Categories where objects are sets, but with extra structure and arrows are functions that preservere that structure. For example, there are categories of (aks the audience what structures they came across)
     - graphs
     - groups
     - commutative groups
     - monoids
     - ordered sets
     - vector spaces
     - metric spaces
     - topological spaces
     - ...
     
  - Categories where objects are data-types and arrows are programs (*type theory*)
     
  - Categories where objects are sets (with extra structure or not) and arrows are not functions but, say, relations
  
  - Categories where objects are not sets, but themselves points in a space and the arrows are paths connecting the points
  
  - Categories where the set of arrows *A(a,b)* is replaced by an object in another category (*enriched category theory*)
  
  - Categories where the both the set of object and the set of arrows are replaced by objects in another category (*internal category theory*)
  
  - Categories that have two or more ways of composing arrows (*monoidal categories, double categories, higher categories*)
  
  While it is the first item that is best known in the mathematical world, it is the other ones that are more interesting as topics of research inside category theory. The last item will play a role in the rest of the talk.
  
- Category theory is the way to go if you want to think "up to isomorphism". (Example: The skeleton of a category.)
  
- Category theory can be understood as a set theory in which you dont use "is an element of" as the basic operation but "composition". This leads to a fantastic idea, namely *definition by universal property*. We have seen that there is a large variety of categories. If you make a definition by "is an element of" then you have to adapt the definition for each category and, by the way, it only works in case your category is of the "objects are sets plus structure" variety. If you make a definition by universal property, then it makes sense in all of these different examples. So category theory can be full of beautiful surprises where seemingly different constructions end up being instance of the same universal property. (Example: cartesian product.)

- (Maybe that needs to be skipped for the talk as it would take to long and is not needed.) One of the most powerful notions of mathematics, comparable to the invention of the 0, is that of a *natural transformation*. It is the notion category theory was created for and plays a central role in the [first paper on the subject](https://ncatlab.org/nlab/show/General+Theory+of+Natural+Equivalences). I will just explain the main idea. In mathematics, early on, you encounter indexed numbers, such as x_i where i runs over an infinite set as eg in Taylor series. Later, one also needs indexed functions f_i. A natural transformation generalises such a family of functions in the case where the indices are not a mere set but a category. This happens all the time in mathematics and I give you just one example. We said that there is a category where objects are data types and arrows are programs. But some data types can be indexed, for example the type List(X) of lists over a set X: The elements of X are the elements you can put in the lists. Now functions 

        f_X: List(X) -> List(X)

from lists to lists are also indexed by X. So which families f_X of indexed functions are natural in this example? The natural transformations are what is called in programming the *polymorphic functions*, that is, the functions that have the same definitions for all X, or, the programs that would run correctly whatever X is. For example, reversing a list is polymorphic (natural), but sorting a list of numbers is not. (Question: For which data type would sorting be polymorphic?)

### Monoidal Categories and String Diagrams

Some comments on 2-Dimensional Algebra ...

A ***monoidal category*** is a category in which we have a second composition on objects and arrows which we write as ... and which satisfies the interchange law ... 



### A 2-Dimensional Calculus of Simultaneous Substitutions

### Summary and Outlook

We have learned quite a bit about category theory and string diagrams

### References



---
---

A review on the relationship between functions and substitutions  ... why this is important ... an indication of why this is subtle 

Would the students find examples from programming helpful (only simple things about variables and calling functions, no recursion)?

If yes, I could launch into the definition of a category from there ... lots of examples (10 min) 

and then go to monoidal categories ... this is not as terrible as it sounds, on the contrary, it makes categories more meaningful and may give students a better grip (10min)

In particular, there is a beautiful graphical calculus for monoidal categories that makes things quite intuitive and natural (10min)

Functions as an example of monoidal categories (10min)

The problem with substitution (10min) ... now this is going to be subtle ... I need to think about how to do this ...

Then we can think about how to extend monoidal categories to substitutions. Now here I can start to not explain everything in detail as the big ideas have been presented and I only need to convince the students that these ideas can be used to solve our problem. (10min)
