# What's in a shopping list?

For the purpose of illustrating key Dbquity concepts, in this example we want to work with lists of items to buy such as milk, potatoes, and bread. And we want to note in which shop we go to get the items on a particular list.

In Dbquity terms, we want a collection of Lists where each List is associated to one or more Item entities, and each list should be able to link to a shop. This can be declared as follows:

<table><tr><td><pre><code>
site ShoppingList
    area Shopping
        entity Shop
            collection: Shops
            text Name
            identity: Name
        entity Item
            collection: Items
            text Name
            identity: Name
        entity List
            collection: Lists
            link Shop
        association ToBuy
            end List
            end Item
                multiplicity: 1..*
</code></pre></td>
<td><img src="ShoppingList.dbquity.svg"/></td></tr></table>

## `entity` models: Item, List, and Shop
Notice that 
1. all three `entity` models declare a `collection`,
2. the Item `entity` model and the Shop `entity` model both declare a `text` Name field which forms their `identity`, and
3. the List `entity` model declares no fields and no `identity`.

We can use this model to illustrate the core semantics of an entity:
> *an `entity` is a structured piece of data, which we can save into its `collection` and then later find again by its `identity`*.

In order for the *find again* piece to work, the `identity` is unique within the `collection`:

- As mentioned, we can have Item entities with distinct names such as "milk", "potatoes", and "bread", but, we cannot have two different Item entities named "bread", because then the collection would not know which "bread" to return when we asked it for the "bread" Item.

- It is however, very possible to have a Shop and an Item both identified as "bread", because Shops and Items are two distinct collections.

The entities declared by the `entity` model List will be assigned increasing (but not necessarily consequtive) integer numbers as their `identity`, because the model does not declare otherwise. 

## `association` model: ToBuy
Declaring the `association` ToBuy enables users to associate Item entities with List entities such that for a List to be considered valid, at least one Item should be associated To Buy as captured by `multiplicity: 1..*` under `end Item`. The other `end` of the association links to List and as depicted in the diagram defaults to a `multiplicity` of `0..*` (or just `*`).

## `link` a List to a Shop
Finally, the ability to link a List to a specific Shop is captured by the line `link Shop`, which does not declare any constraints, meaning that any List entity may be linked to a single Shop.

## Diagram a model
The Dbquity [CLI](https://model.dbquity.com/#command-line-interface-cli) includes a `dot` command, which produces `.dot` files as defined by [Graphviz](https://graphviz.org) from models.

You can see the full syntax for the command by typing `dbquity dot ?` in a prompt.

However, it is often more convenient to use the `draw.bat` batch command that comes as part of the [CLI](https://model.dbquity.com/#command-line-interface-cli).

`draw.bat` first calls the [CLI](https://model.dbquity.com/#command-line-interface-cli) to produce the `.dot` file, then uses a Graphviz tool called `dot.exe` to produce an `.svg`-file, which it finally opens in the default browser.

In case you have not yet installed Graphviz, `draw.bat` will direct you to [a hint page](https://model.dbquity.com/svgfail?dotfile=mymodel) with helpful links.

`draw.bat` uses a simple syntax: `draw <model-name> <options>` where <options> are passed on to the [CLI](https://model.dbquity.com/#command-line-interface-cli) for controlling how the `.dot` file is generated.

For example, `draw ShoppingList +m -r -nolabel` produces the diagram from the top of this page:

![Diagram showing the structure of the ShoppingList sample model](ShoppingList.dbquity.svg)

If you have several `.dbquity`-files in the current directory, you may find `diagrams.bat` useful, and `svg.bat` gives you more fine-grained control than `draw.bat`.

Finally, `dot2svg.bat` is for when you have manually edited the `.dot` file.

Happy diagramming :-)

## [CLI](https://model.dbquity.com/#command-line-interface-cli) commands for import, export and validation of site data
The [CLI](https://model.dbquity.com/#command-line-interface-cli) includes these commands that you may run against a local test site:
|to...|issue this command|
|---|---|
|validate all data|`dbquity validate <sitename>`|
|export all data to a file|`dbquity export <sitename> [<filename>[.dbquity-data]]`|
|import dataset(s)|`dbquity import <sitename> [<datafile>[.dbquity-data] [<datafile2>[.dbquity-data] ...]]`|

[ShoppingList.dbquity-data](ShoppingList.dbquity-data) is an example of `.dbquity-data`-file.
