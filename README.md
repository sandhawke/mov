# mov: an RDF Schema for making movable RDF schemas

This schema is helpful for writing "movable" RDF schemas. Schemas (also called ontologies or vocabulary definitions) which are movable retain their semantics even when moved to different URLs.  For example, while the original version of this document is hosted at <https://sandhawke.github.io/mov>, it is possible (and recommended) to use this schema in other ways which do not involve trusting either github or the author (such as by forking it or copying it to your own server).

In fact, due to limitions of github hosting, the namespace URL for this schema is different for different formats.  This would normally break interoperability, but with movable schemas, it's fine.

The provided formats and locations/namespaces are:

|Format|Media Type|Namespace URL|
|:----:|:---:|:------------|
|Turtle|text/turtle|<https://sandhawke.github.io/mov/schema.ttl#>
|JSON-LD|application/ld+json|<https://sandhawke.github.io/mov/schema.jsonld#>
|JSON-LD embedded in HTML|text/html|<https://sandhawke.github.io/mov#>

For JSON-LD, the location/namespace is also the @context URL.

## Concept

The basic concept is that we identify each RDF property (and class, etc) using some definition text, not its URI. It still has a URI, but the URI doesn't have to match other occurances of the property (in other data sources, or in data-consuming software), because the match will also be done using the definition text.  This additional matching is specified in OWL, but the implementation is simple and not require using or understanding OWL.

## Practice

In practice, to create a movable schema, you need to provide suitable definition text for each resource in your schema using this mov schema.  The definition should be a few lines of text, specifying the item well enough that a careful expert reader who is confident they understand the text is quite unlikely to be wrong in any observable way.

## Terms

### mov:itemdef

This can be used for defining any resource.  In practice, it should only be used for resources which are _not_ an rdf:Property or an rdf:Class, since they are more easily defined using mov:propdef and mov:classdef.


### mov:propdef

### mov:classdef

<script type="application/ld+json">
// schema.jsonld should be copied here
</script>