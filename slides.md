% TDD as in Type-Directed Development
% Clément Delafargue
% scala.io 2014-10-24

-------------------------------------------

# <span style="font-size: 8em;">λ</span>

-------------------------------------------

![](/Users/clementd/Projects/perso/gifs/forrest.jpg)

-------------------------------------------

## Example time

-------------------------------------------

# Example time

```
GET /endpoint?number=5

10
```

-------------------------------------------

```scala

def addFiveAction(
    params: Map[String, String]
) = {

    val nbS = params("number")
    if(nbS != "") {
        val nb = nbS.toInt
        nb + 5
    } else {
        0
    }
}

```

-------------------------------------------

```scala

addFiveAction(Map("number" -> "12"));
    // 17

addFiveAction(Map("yolo" -> "12"));
    // java.lang.NullPointerException

addFiveAction(Map("number" -> "yolo"));
    // java.lang.NumberFormatException

```

-------------------------------------------

# Pokemon Driven Development
<video src="/Users/clementd/Projects/perso/gifs/cat-clothes.webm" autoplay loop/>

-------------------------------------------

<div style="font-size: 0.8em;">

```scala

def addFiveAction(
  params: Map[String, String]) = {
    val nbS = params("number")

    if(nbS != null) {
        if(!nbS != "") {
            try {
                val nb = nbS.toInt
                nb + 5
            } catch {
                case e: NumberFormatException e => 0
            }
        }
    } else {
        0
    }
}

```
</div>

-------------------------------------------

## De plous en plous difficile

-------------------------------------------

# De plous en plous difficile

```
GET /endoint?n1=20&n2=22

42
```

-------------------------------------------

<div style="font-size: 0.5em;">

```scala

def addNumbersAction(
  params: Map[String, String]) = {
    val nbS1 = params("n1");
    val nbS2 = params("n2");

    if(nbS1 != null) {
        if(!nbS1 != "") {
            try {
                val nb1 = nbS1.toInt
                if(nbS2 != null) {
                    if(!nbS2 != "") {
                        try {
                            val nb2 = nbS2.toInt
                            nbS1 + nbS2
                        } catch {
                            case e: NumberFormatException => 0
                        }
                    }
                }
            } catch {
                case e: NumberFormatException => 0
            }
        }
    } else {
        0
    }
}

```
</div>

-------------------------------------------

![](assets/carrie.jpg)

-------------------------------------------

## Thinking with types

-------------------------------------------

## From a map, I can get a value…

-------------------------------------------

## `maybe`

-------------------------------------------

```scala
def getKeyAt(
    values: Map[String,String],
    key: String
): MaybeString
```

-------------------------------------------

## From a string, I can get an int…

-------------------------------------------

## `maybe`

-------------------------------------------

```scala
def parseInt(
    str: String
): MaybeInt
```
-------------------------------------------

![](assets/option.png)

-------------------------------------------


```scala

def parseInt(str: String):
  Option[Int]

map[A,B]#get(key: A): Option[B]
```

-------------------------------------------

```scala
def getInt(
    index: String,
    vals: Map[String, String]
): Option[Int]
```

-------------------------------------------

![](assets/flatmap.png)

-------------------------------------------

<div style="font-size: 0.9em;">
```scala
def addNumbersAction(
  params: Map[String, String]
): Int = {
    val i1 = getInt("n1", params)
    val i2 = getInt("n2", params)
    i1.getOrElse(0) + i2.getOrElse(0)
}

```

</div>

-------------------------------------------

<div style="font-size: 0.5em;">

```scala

def addNumbersAction(
  params: Map[String, String]) = {
    val nbS1 = params("n1");
    val nbS2 = params("n2");

    if(nbS1 != null) {
        if(!nbS1 != "") {
            try {
                val nb1 = nbS1.toInt
                if(nbS2 != null) {
                    if(!nbS2 != "") {
                        try {
                            val nb2 = nbS2.toInt
                            nbS1 + nbS2
                        } catch {
                            case e: NumberFormatException => 0
                        }
                    }
                }
            } catch {
                case e: NumberFormatException => 0
            }
        }
    } else {
        0
    }
}

```
</div>

-------------------------------------------

<video src="/Users/clementd/Projects/perso/gifs/computer-ok.webm" autoplay loop/>

-------------------------------------------

## Correct…

-------------------------------------------

## By construction

-------------------------------------------

<video src="/Users/clementd/Projects/perso/gifs/computer-no.webm" autoplay loop/>

-------------------------------------------

## Why not tests?

-------------------------------------------

## Why not <i>only</i> tests?

-------------------------------------------

# <span style="font-size: 5.5em;">∃</span><br>« there exists »

-------------------------------------------

## `Int -> Int`

-------------------------------------------

## `2`<sup>`32`</sup>

-------------------------------------------

## `2`<sup>`64`</sup>

-------------------------------------------

## `String -> String`

-------------------------------------------

## `∞`

-------------------------------------------

## `∞` (ish)

-------------------------------------------

# <span style="font-size: 5.5em;">∀</span><br>« for all »

-------------------------------------------

## Type &hArr; Property

-------------------------------------------

## Program &hArr; Proof

-------------------------------------------

## provably > probably

-------------------------------------------

## Expressive type systems

-------------------------------------------

## Everything is an expression

-------------------------------------------

## Typed Control structures

-------------------------------------------

# Homogeneous branches

```scala




val myValue = if(expression) {
  "if true"
} else {
  "if false"
}
```

-------------------------------------------

# Typed loops

```scala



val myList =
  for(x <- xs)
  yield x * 2
```

-------------------------------------------

# Avoid stupid mistakes

```c



if(error)
  goto fail;
  goto fail;
```

-------------------------------------------

## Maybe

-------------------------------------------

## NonEmptyList

-------------------------------------------

## Validation

-------------------------------------------

## `newtype` + smart constructors

-------------------------------------------

## tagged types

-------------------------------------------

```scala
sealed trait Meter
sealed trait Mile

type RegularLength = Int @@ Meter
type ImperialGobbledygook = Int @@ Mile


val marsProbeAltitude: RegularLength = …
```

-------------------------------------------

## Memory management

-------------------------------------------

## Resource management

-------------------------------------------

## Parametricity

-------------------------------------------

## Parametricity<br>(aka generics)

-------------------------------------------

# Ignorance is bliss

<video src="/Users/clementd/Projects/perso/gifs/i-dont-care.webm" autoplay loop/>

-------------------------------------------

# Parametricity

```scala


def f(
    x: A
): A

```

-------------------------------------------

# Parametricity

```scala


def compose[A,B,C](
    g: (B => C),
    f: (A => B)
): (A => C)

```

-------------------------------------------

# Parametricity

```scala


def reverse[A](
    xs: List[A]
): List[A]

```

-------------------------------------------

## `reverse(Nil) == Nil`

-------------------------------------------

## `reverse(xs).contains(a)`<br>`=>`<br>`xs.contains(a)`

-------------------------------------------

## Theorems for free
<video src="/Users/clementd/Projects/perso/gifs/money.webm" autoplay loop/>

-------------------------------------------

```scala
trait List[A] {
    def filter(p: A => Boolean): List[A]

    def map[B](f: A => B): List[B]
}

l.filter(compose(p,f)).map(f) ==
l.map(f).filter(p)
```

-------------------------------------------

## Discipline

-------------------------------------------

# no `null`s
<video src="/Users/clementd/Projects/perso/gifs/bang-boom.webm" autoplay loop/>

-------------------------------------------

## `Type <=> Property`

-------------------------------------------

## `null` can inhabit any type

-------------------------------------------

## `null` can prove every property

-------------------------------------------

## No exceptions

-------------------------------------------

# no reflection

<video src="/Users/clementd/Projects/perso/gifs/bicycle-gorilla.webm" autoplay loop/>

-------------------------------------------

## Reflection breaks blissful ignorance

-------------------------------------------

# Reflection

```scala


def f[A](x: A): String
```

-------------------------------------------

```scala
def f[A](x: A): String =

x match {
  case v: String => v
  case v: Int => "int"
  case _ => "whatever"
}
```

-------------------------------------------

# no `toString` / `equals` / `hashCode`
<video src="/Users/clementd/Projects/perso/gifs/driving-fail.webm" autoplay loop/>

-------------------------------------------

```scala
def f[A](x: A): String =
x.toString
```

-------------------------------------------

# Side effects
<video src="/Users/clementd/Projects/perso/gifs/sam-sad.webm" autoplay loop/>

-------------------------------------------

```scala
def f[A](x: A): String = {
  donaldTrump.sendTweet()
  launchBallisticMissile()

  System.getenv("JAVA_HOME")
}
```

-------------------------------------------

## Fast and loose reasoning is morally correct

-------------------------------------------

## <i>Type</i>-Directed Development

-------------------------------------------

## Not a silver bullet

-------------------------------------------

## Just helpful

-------------------------------------------

## Confidence

-------------------------------------------

# Modular thinking

<video src="/Users/clementd/Projects/perso/gifs/bunny-nom.webm" autoplay loop/>

-------------------------------------------

## Not just about safety

-------------------------------------------

## Types help with structure

-------------------------------------------

## Ensure consistency, step by step

-------------------------------------------

```scala
def myMethod(a: Input): Output = ???

def myOtherMethod(
  a: List[Input]
): List[Output] = {

  a.map(myMethod)

}
```

-------------------------------------------

## Type check `/=`Compilation

# Hole-Driven-Development

<video src="/Users/clementd/Projects/perso/gifs/abyss.webm" autoplay loop/>

-------------------------------------------

```scala
case object Hole

def compose[A,B,C](
    g: (B => C),
    f: (A => B)
): (A => C) = Hole
```

Hole has type `A => C`

-------------------------------------------

```scala

def compose[A,B,C](
    g: (B => C),
    f: (A => B)
): (A => C) = (x: A) => Hole
```

`x` has type `A`  
Hole has type `C`

-------------------------------------------

```scala
def compose[A,B,C](
    g: (B => C),
    f: (A => B)
): (A => C) = (x: A) => g(Hole)
```

`X` has type `A`  
Hole has type `B`

-------------------------------------------

```scala
def compose[A,B,C](
    g: (B => C),
    f: (A => B)
): (A => C) = (x: A) => g(f(Hole))
```

`x` has type `A`  
Hole has type `A`  
`Hole = x`

-------------------------------------------

```scala

def compose[A,B,C](
    g: (B => C),
    f: (A => B)
): (A => C) = (x: A) => g(f(x))

```

-------------------------------------------

## Test-driven development

-------------------------------------------

## Red / Green / Refactor

-------------------------------------------

## Type / Define / Refine

-------------------------------------------

## Types make communication easy

-------------------------------------------

## With machines

-------------------------------------------

## Type checking

-------------------------------------------

# Tooling

<video src="/Users/clementd/Projects/perso/gifs/hammer.webm" autoplay loop/>

-------------------------------------------

<div style="background-color: blue; width: 100%; height: 100%">
<h3><span style="font-family: 'Comic Sans MS'; color: yellow;">Haskell type syntax</span></h3>
</div>

-------------------------------------------

## `a -> a`

-------------------------------------------

## `Int -> Int`

-------------------------------------------

## `a -> b -> a`

-------------------------------------------

## `(a, b) -> a`

-------------------------------------------

## `a -> (b -> a)`

-------------------------------------------

## `(Ord a) => [a] -> [a]`

-------------------------------------------

## Intent

-------------------------------------------

# Hoogle <3 <3

<http://www.haskell.org/hoogle>

-------------------------------------------

## Remove duplicates

-------------------------------------------

## `Eq a => [a] -> [a]`

-------------------------------------------

<video src="./assets/hoogle1.mkv" autoplay loop/>

-------------------------------------------

## `[Maybe a] -> Maybe [a]`

-------------------------------------------

<video src="./assets/hoogle2.mkv" autoplay loop/>

-------------------------------------------

## With humans

-------------------------------------------

## Types can't always prove everything

-------------------------------------------

## And that's ok

-------------------------------------------

```scala
def reverse[A](
    xs: List[A]
): List[A]
```

-------------------------------------------

<div style="font-size: 1.2em;">

```scala

def reverseProp[A: Equal](
  xs: List[A],
  ys: List[A]
) = {

    reverse(xs ++ ys) ==
    reverse(ys) ++ reverse(xs)
}
```

</div>

-------------------------------------------

<div style="font-size: 1.2em;">

```scala

def reverseProp2[A: Equal](
  xs: List[A]
) = {

    reverse(xs).length ==
    xs.length
}
```

</div>

-------------------------------------------

## Property-based reasoning

-------------------------------------------

## <span style="font-size: 5.5em;">∀</span>(ish)

-------------------------------------------

## Perfect for edge 

-------------------------------------------

## Test the specification

-------------------------------------------

Types *then*

Property-based tests *then*

Unit tests

-------------------------------------------

![](./assets/pyramid.png)

-------------------------------------------

## Lay out the function types

-------------------------------------------

## Write property-based tests

-------------------------------------------

## Operations + laws

-------------------------------------------

<video src="/Users/clementd/Projects/perso/gifs/math.webm" autoplay loop/>

-------------------------------------------

## Algebra

-------------------------------------------

## Figure out data structures

-------------------------------------------

## Implement

-------------------------------------------

## Unit test for regressions

-------------------------------------------

## `???`

-------------------------------------------

## Profit

-------------------------------------------

## Types are

-------------------------------------------

## Safety feature

-------------------------------------------

## High-level reasonning tool

-------------------------------------------

## Communication tool

-------------------------------------------

## So let's use them!

-------------------------------------------

# Read this

- [TAPL](http://www.cis.upenn.edu/~bcpierce/tapl/)
- [PFPL](http://www.cs.cmu.edu/~rwh/plbook/book.pdf)

-------------------------------------------

# Read this

- [FP in Scala (aka the Red Book)](http://manning.com/bjarnason)

-------------------------------------------

# Read this

- [Functional and Reactive Domain Modelling](http://manning.com/ghosh2/)

-------------------------------------------

## Try Rust

-------------------------------------------

## Try Idris

-------------------------------------------

## Thanks!

-------------------------------------------

- [\@clementd](https://twitter.com/clementd)
- [cltdl.fr/me](https://cltdl.fr/me)