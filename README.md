This schema is helpful for writing "movable" RDF schemas. (We use the term "schema" to include "ontology" and "vocabulary definition", since the terms are equivalent in this context.) RDF schemas are generally useful for providing interoperability between loosely coupled systems, but they require URLs which remain stable over many years.

Movable schemas, in contrast, allow interoperability even when moved to different URLs.  For example, while the original version of this document was (and perhaps still is) hosted at <https://sandhawke.github.io/mov>, it is possible (and recommended) to use this schema in ways which do not involve trusting either github or the author, such as by forking it or copying it to your own server.

**In fact, due to limitions of github hosting, the namespace URL for this schema is different for different formats.  This would normally break interoperability, but with movable schemas, it's fine.**

The provided formats and locations/namespaces are:

|Format|Media Type|Namespace URL|
|:----:|:---:|:------------|
|Turtle|text/turtle|<https://sandhawke.github.io/mov/schema.ttl#>
|JSON-LD|application/ld+json|<https://sandhawke.github.io/mov/schema.jsonld#>
|JSON-LD embedded in HTML|text/html|<https://sandhawke.github.io/mov#>

For JSON-LD, the location/namespace is also the @context URL.

## Concept

The basic concept is that we identify each RDF property (and class, etc) using some definition text, not its URI. It still has a URI, but the URI doesn't have to match other references to the property, because the match will also be done using the definition text.  What's needed is that each data source being merged, and each system consuming the data, use the same definition text.  In some ways this is more cumbersome than using the same URI, but in other ways it is simpler.

## Practice

In practice, to create a movable schema, you need to provide suitable definition text for each resource in your schema using this **mov** schema.  The definition should be a few lines of text, specifying the item well enough that a careful expert reader who is confident they understand the text is very likely to be right.  (For machine purposes, the important thing is that the text has enough entropy that it is statistically unlikely to accidentally be the same as someone else's definition of another term.  By requiring the definitions to be meaningful and unambiguous to people, the same string should only be coincidentally selected when the meaning is the same.)

These definitions can be embedded in your data or provided nearby, like by a schema file in the same directory. You can also point to the original provider, as you would be with a non-movable schema, if you happen to trust them sufficiently.

To consume movable schemas, with all the data integration benefits of non-movable schemas, an additional software layer is required to first do the merging based on definition matches.  This layer can be built into tools or executed before the data is loaded into conventional tools.   (It might be possible to build a translating proxy, but https would make this very difficult.)

## Terms

### **mov:itemdef**

This can be used for defining any resource.  In practice, it should only be used for resources which are _not_ an rdf:Property or an rdfs:Class, since they are more easily defined using mov:propdef and mov:classdef.

Example:

```turtle
PREFIX mov: <https://sandhawke.github.io/mov/schema.ttl#>
PREFIX : <.#>
:Tatooine mov:itemdef "A fictional location, a planet called 'Tatooine' in the Star Wars franchise. It was introduced in the 1977 film _Star Wars_ as the home of protagonist Luke Skywalker.".
```

### **mov:propdef**

This is used for defining RDF properties, such that they can be textually matched even when using different URIs.

Example 1:

```turtle
PREFIX mov: <https://sandhawke.github.io/mov/schema.ttl#>
PREFIX : <.#>
:familyName mov:propdef "The family name of some person. This name is usually assigned at birth, identical to or derived from the parents' family names. Siblings in the same family are usually given the same family name, and family names usually only change with adoption or, for some people in some cultures, marriage. Typically, a person's name is their family name and given name combined in an order that depends on context.".
```

Example 2, using a template-style definition, instead of dictionary-style. This example uses the feature that matching ignores contents in square brackets, and pushes the limit of short definitions. Given the wide consensus on what "family name" means, this is probably okay for most applications.

```turtle
PREFIX mov: <https://sandhawke.github.io/mov/schema.ttl#>
PREFIX : <.#>
:familyName mov:propdef "[subject ref] has the family name [value string].".
```

### **mov:classdef**

tbd

## Modifying your definitions

Often, after some experience using term definitions you developed, you will think of better wording, or otherwise want to change the text. We suggest keeping the old wording if anyone might be using it or interested in it, and just adding the new wording, as a new definition.

There are two ways to add these new defintions:

1. If the change is purely **editorial** and does not reflect a change in your intended meaning, then the change is nonbreaking.  You can simply add the new definition to the same term.  This asserts you consider the definitions to be synonymous.

2. If the change does reflect a change in your intended meaning, then it is **substantive** and is a breaking change. If systems conflate the two meanings, they might get incorrect results. For a change like this, you need to make up a new term URI and put the new definition on that term.  (You can rename terms if, and only if, all supported consumers are movable-schema-aware.)

Consumers do have the ability to override your decision, above, in that they can choose which definitions to use for each of the terms they consume. When you treat the change as editorial/nonbreaking, they might decided not to use one of the definitions you equate, because they do not consider them sufficiently synonymous.  Alternatively, if you treat the change as substantive/breaking, they might decide for their application the definitions are close enough and equate them.

## Implementations

[schemove](https://github.com/sandhawke/schemove)

## Technical Details

...

<hr />

<script>
// Text below this line is intended to be hidden, but may show up on some systems.  Please ignore it.
</script>

<hr />

<script type="application/ld+json">
// schema.jsonld should be copied here
</script>

<script type="text/turtle">
// schema.ttl should be copied here
</script>