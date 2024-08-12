# AI about the HelloWorld model source

Here is what Microsoft's Copilot had to say about the [HelloWorld](HelloWorld.dbquity) `site model` on a rainy spring day in April 2024:

<i>
The Dbquity Modeling Language is an interesting tool! Let’s break down the information from the selected text:

1. Site Description:
    - The site is named “HelloWorld” and is located at model.dbquity.com/examples.
    - It’s version 1.0.0.
    - The site illustrates various concepts such as classes, invariants, areas, and multiline text.
2. Class: Period:
    - The Period class represents an interval of a certain number of days.
    - It has three fields:
        - Start: A date field that initializes to today’s date by default.
        - Days: An integer field representing the number of days in the interval.
        - End: Another date field.
    - The class uses an invariant property:
        - Start + Days = End (the interval is consistent).
        - Start <= End (the start date is before or equal to the end date).
3. Area: Welcome:
    - Contains a Period instance named Meeting.
    - Also includes a multiline text field called Greeting with a placeholder for kind words (emoji allowed).

Overall, Dbquity seems to be a powerful modeling language for capturing and managing data structures.
</i>

# Inventor's comments

As the inventor of Dbquity, I enjoyed reading that break-down and I hope that repeating it here conveys that the idea of the Dbquity language is to be both concise and intuitive.

For ease of reference, this is a condensed version of the HelloWorld site model stripped from `description` properties and comments:
```dbquity
site HelloWorld
    location: model.dbquity.com/examples
    version: 1.0.0
    class Period
        date Start
        integer Days
        date End
        invariant: Start + Days = End and Start <= End
    area Welcome
        Period Meeting
        text Greeting
            multiline
            placeholder: ...
```

> Note, that the `location` property has since been renamed `origin`.

## indentation defines model composition and is reflected in the UI 
Indentation is key in capturing the *structure* of a Dbquity `site`.

Making use of the `class` Period declared at the beginning, this particular `site` has a simple structure consisting of the a single `area` **Welcome** with two fields `Period` **Meeting** and `text` **Greeting** as you see in this screenshot:

![](HelloWorld.PNG)

> In general, any content of a Dbquity `site` belong to an `area` of which a site may have one or more as declared by the models that have been deployed to that site.

## the model is it!
Another fact to know about Dbquity is that a site model is the only source artefact needed to deploy and run a site on your favourite cloud storage and invite others to share the data stored on that site.

To deploy HelloWorld.dbquity to a site called hello on your local harddisk use this [CLI](https://model.dbquity.com/#command-line-interface-cli) command:

```bat
dbquity deploy hello -caption:"Salute!" HelloWorld.dbquity
```
> Now, if you look in your
> ```
> %LOCALAPPDATA%\Dbquity\
> ```
> folder, you'll find a subfolder called `hello.test` where `.test` signifies that the site is meant for testing locally thru the Dbquity UI before publishing the model for others to deploy to "real" sites.

Once that is done, run the [TestUI](https://model.dbquity.com/#test-ui) and [Go] to the hello test site.

## declarative vs imperative
Next, try to interact with the Start, Days and End fields of the Meeting and notice how changing one updates another thanks to the `invariant` property declared on the Period `class`. No need to author three separate pieces of code, one for each field, and keep them consistent.

Thus, this invariant is meant to illustrate a maintainability point about being as declarative as possible.
<? Dbquity is built prefering declarative over imperative approaches, and as a rule of thumb, I personally recommend declarativeness whenever possible - also when it comes to crafting Dbquity models :-)  
Still, Dbquity *does* support imperative code when declaring the `execution` property of an `action` or the `behaviour` of a `step` whilst the combined `behaviour` of an `entity` is declared as a single expression orchestrating the steps that the `entity` declare. ?>

## curious for more?
You might then take a look at the [ShoppingList](../ShoppingList/README.md) example, which introduces the key notions of `entity`, `association`, and `link` and talks about diagramming a model and exporting and importing data from/to a local test site...


Cheers  
*Lars*

### a comment on `#`-comments
The Dbquity language supports rest-of-line comments using the hash symbol `#`, e.g.:
```dbquity
date Start    # initializes to today() by default
```
where the whitespace leading up to the `#`, the `#` itself as well as the rest of that line will be ignored.  

Some languages include a syntax for multi-line comments. Dbquity only supports these rest-of-line comments, which may come in consequtive groups, e.g.:
```dbquity
# when a user changes one value, Dbquity seeks to update another as
# needed to satisfy the invariant
invariant:                                    
    Start + Days = End and Start <= End
```
