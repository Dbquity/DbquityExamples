# Dbquity Examples
This repository contains select sample models illustrating modeling capabilities of [Dbquity](https://model.dbquity.com) and introduces you to some features of the modelers' tooling.

For each of the examples, model source and other relevant files are provided, and a readme is put together to explain some of the modeling and tooling features used.

## HelloWorld
Any language needs a *Hello World* example - including the Dbquity Modeling Language :-)

This comprehensive first example:
1. introduces the modeling notions `site`, `area`, `class`, `field`, and `invariant`,  
2. uses the [Command Line Interface (CLI)](https://model.dbquity.com/#command-line-interface-cli) to deploy a model to a local test *site*,
3. shows how to access the *site* - like an end-user would - through the [TestUI](https://model.dbquity.com/#test-ui).

Read it all [here](HelloWorld/README.md).

## ShoppingList
Looking at a model comprising multiple entities, the notions of `entity`, `association`, and `link` are introduced, and it is demonstrated how to diagram a model, and export and import data from/to a deployed site.

See the [Shopping List readme](ShoppingList/README.md) for a discussion of these features.

## RollDice
The [RollDice readme](behaviour/README.md) walks through a model of a simple toss a die game and proposes a declarative approach to logic using the notions of `behaviour` and `step`.

Then, it demonstrates how to test RollDice using the automated test features of Dbquity.

## WebWordle
A variant of the well-known Wordle game that let's multiple players compete on guessing words off a webpage rather than from a dictionary.

This game came about as a very welcome challenge to the Dbquity modeling capabilities raised by [@nkyaelly](https://github.com/nkyaelly)  :-) :-) :-)

Read about WebWordle and take on a "key" challenge of your own [here][wordle-readme]. 

[wordle-readme]: WebWordle/README.md
