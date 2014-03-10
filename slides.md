% TDD, as in Type-Directed Development
% Clément Delafargue
% 2014-04-11

-------------------------------------------

# Who am I?

Architect / Developer / Teacher

-------------------------------------------

![](assets/forrest.jpg)

-------------------------------------------

# X-Driven Development

-------------------------------------------

Code-Driven Development?

-------------------------------------------

LOLNOPE

-------------------------------------------

Why?

-------------------------------------------

Smaller bites

-------------------------------------------

CONFIDENCE

-------------------------------------------

Test-Driven Development?

-------------------------------------------

Good…

-------------------------------------------

… but not enough

-------------------------------------------

<span style="font-size: 5.5em;">&exist;</span>

« there exists »

-------------------------------------------

<span style="font-size: 5.5em;">&forall;</span>

« for all »


-------------------------------------------

# Type-Directed Development

-------------------------------------------

Mythbuster

-------------------------------------------

Expressive type systems

-------------------------------------------

Type inference

-------------------------------------------

<div style="font-size: 1.5em;">

```haskell

myVar =
    "obviously a string"

myVar = [ "obviously"
        , "a"
        , "list"
        , "of"
        , "strings"
        ]

```
</div>

-------------------------------------------

Type &hArr; Property

Program &hArr; Proof

-------------------------------------------

Obviously correct programs

Don't fix bugs, make them impossible

-------------------------------------------

<div style="font-size: 2em;">

```haskell

data Option a =
     Some a
   | None

```
</div>

-------------------------------------------

<div style="font-size: 2em;">

```haskell

mapOption ::
    ( Option a
    , (a -> b)
    ) ->
    Option b

```
</div>

-------------------------------------------

<div style="font-size: 2em;">

```haskell

data NEList a = {
    head :: a,
    tail :: [a]
}
```
</div>

-------------------------------------------

<div style="font-size: 2em;">

```haskell

mapNEL ::
    ( NEList a
    , (a -> b)
    ) ->
    NEList b

```
</div>

-------------------------------------------

Parametricity

-------------------------------------------

<div style="font-size: 2em;">

```haskell

reverse ::
    [a] -> [a]

```
</div>

-------------------------------------------

Types are the best doc

Hoogle

-------------------------------------------

Types can't always prove everything

-------------------------------------------

And that's ok

-------------------------------------------

<div style="font-size: 1.2em;">

```haskell

reverseProp ::
    Eq a =>
    [a] -> [a] -> Bool
reverseProp xs ys =
    reverse (xs ++ ys) ==
        reverse ys ++ reverse xs
```

    λ> quickCheck reverseProp
    +++OK, passed 100 tests.

</div>

-------------------------------------------

Types *then*

Property-based tests *then*

Unit tests

-------------------------------------------

Thanks

-------------------------------------------

[Parametricity](http://dl.dropboxusercontent.com/u/7810909/media/doc/parametricity.pdf)

<http://haskell.org>

