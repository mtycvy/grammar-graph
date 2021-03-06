## Classes

<dl>
<dt><a href="#DecisionGraph">DecisionGraph</a></dt>
<dd></dd>
<dt><a href="#GrammarGraph">GrammarGraph</a></dt>
<dd></dd>
<dt><a href="#GuidedDecisionGraph">GuidedDecisionGraph</a></dt>
<dd></dd>
<dt><a href="#Recognizer">Recognizer</a></dt>
<dd></dd>
</dl>

## Functions

<dl>
<dt><a href="#noSelfDefinitions">noSelfDefinitions(grammar, returns)</a></dt>
<dd><p>check a grammar for direct self-loops</p>
</dd>
<dt><a href="#parseGrammar">parseGrammar(grammar, [seperator])</a> ⇒ <code><a href="#DecisionGraph">DecisionGraph</a></code></dt>
<dd><p>parse a grammar given as an object and compile it into a decision graph</p>
</dd>
<dt><a href="#reduceGrammar">reduceGrammar(grammar, [seperator])</a> ⇒ <code>object</code></dt>
<dd><p>reduces the rules of a grammar into a one to one form by assigning a name
to all non-terminals. The end result is that each option on a rule with
more than one choice will either be a single AND-rule or a single terminal.</p>
</dd>
<dt><a href="#clone">clone(obj)</a> ⇒ <code>object</code> | <code>array</code></dt>
<dd><p>helper function to clone a simple object/array made up of primitives.
Will not work if the object or array contains non-primitives.</p>
</dd>
</dl>

## Typedefs

<dl>
<dt><a href="#SymbolChain">SymbolChain</a> : <code>string</code></dt>
<dd><p>a string of one or more symbol names seperated by whitespace or
another user defined seperator (see: seperator param for <a href="#GrammarGraph">GrammarGraph</a>)</p>
</dd>
<dt><a href="#Grammar">Grammar</a> : <code>Object</code></dt>
<dd><p>a user defined context-free grammar formatted as an object consisting of key-value pairs,
with each <a href="https://github.com/jrleszcz/grammar-graph#non-terminal-symbols">non-terminal symbol</a>
pointing to an array of one or more <a href="https://github.com/jrleszcz/grammar-graph#symbol-chains">symbol chains</a>
choices for this non-terminal.</p>
</dd>
<dt><a href="#TreeNode">TreeNode</a> : <code>object</code></dt>
<dd></dd>
</dl>

<a name="DecisionGraph"></a>
## DecisionGraph
**Kind**: global class  

* [DecisionGraph](#DecisionGraph)
    * [new DecisionGraph()](#new_DecisionGraph_new)
    * [.addVertexAND(name)](#DecisionGraph+addVertexAND)
    * [.addVertexOR(name)](#DecisionGraph+addVertexOR)
    * [.addEdge(v, w)](#DecisionGraph+addEdge)
    * [.adj(v)](#DecisionGraph+adj) ⇒ <code>Array.&lt;string&gt;</code>
    * [.V()](#DecisionGraph+V) ⇒ <code>number</code>
    * [.isTerminal(v)](#DecisionGraph+isTerminal) ⇒ <code>boolean</code>
    * [.isVertex(v)](#DecisionGraph+isVertex) ⇒ <code>boolean</code>
    * [.isTypeAND(v)](#DecisionGraph+isTypeAND) ⇒ <code>boolean</code>
    * [.vertices()](#DecisionGraph+vertices) ⇒ <code>Array.&lt;string&gt;</code>

<a name="new_DecisionGraph_new"></a>
### new DecisionGraph()
creates a new DecisionGraph

<a name="DecisionGraph+addVertexAND"></a>
### decisionGraph.addVertexAND(name)
add AND vertex to the graph. When moving through the decision graph, an AND vertex
will require a visit down each of its outgoing edges, in the order the edges were
added.

**Kind**: instance method of <code>[DecisionGraph](#DecisionGraph)</code>  
**See**: [addVertexOR](#DecisionGraph+addVertexOR)  

| Param | Type | Description |
| --- | --- | --- |
| name | <code>string</code> | the name of this vertex |

<a name="DecisionGraph+addVertexOR"></a>
### decisionGraph.addVertexOR(name)
add OR vertex to the graph. When moving through the decision graph, an OR vertex
chooses just one of its outgoing vertices.

**Kind**: instance method of <code>[DecisionGraph](#DecisionGraph)</code>  
**See**: [addVertexAND](#DecisionGraph+addVertexAND)  

| Param | Type | Description |
| --- | --- | --- |
| name | <code>string</code> | the name of this vertex |

<a name="DecisionGraph+addEdge"></a>
### decisionGraph.addEdge(v, w)
add edge v->w to the graph

**Kind**: instance method of <code>[DecisionGraph](#DecisionGraph)</code>  

| Param | Type | Description |
| --- | --- | --- |
| v | <code>string</code> | the name of a vertex this edge points from |
| w | <code>string</code> &#124; <code>Array.&lt;string&gt;</code> | the name of a vertex this edge points to or an array of vertex names. If vertex v is type AND, the order of w will be the exact order required. |

<a name="DecisionGraph+adj"></a>
### decisionGraph.adj(v) ⇒ <code>Array.&lt;string&gt;</code>
get an array of all the vertices this vertex points to

**Kind**: instance method of <code>[DecisionGraph](#DecisionGraph)</code>  
**Returns**: <code>Array.&lt;string&gt;</code> - an ordered list of all the vertices that v points to  

| Param | Type | Description |
| --- | --- | --- |
| v | <code>string</code> | the name of a vertex |

<a name="DecisionGraph+V"></a>
### decisionGraph.V() ⇒ <code>number</code>
get the number of vertices in this graph

**Kind**: instance method of <code>[DecisionGraph](#DecisionGraph)</code>  
**Returns**: <code>number</code> - the number of vertices in this graph  
<a name="DecisionGraph+isTerminal"></a>
### decisionGraph.isTerminal(v) ⇒ <code>boolean</code>
is this a terminal vertex (does it have no outgoing edges?)

**Kind**: instance method of <code>[DecisionGraph](#DecisionGraph)</code>  
**Returns**: <code>boolean</code> - is this a terminal vertex  

| Param | Type | Description |
| --- | --- | --- |
| v | <code>string</code> | the name of a vertex |

<a name="DecisionGraph+isVertex"></a>
### decisionGraph.isVertex(v) ⇒ <code>boolean</code>
is this the name of a vertex in the graph?

**Kind**: instance method of <code>[DecisionGraph](#DecisionGraph)</code>  
**Returns**: <code>boolean</code> - is this a vertex in the graph  

| Param | Type | Description |
| --- | --- | --- |
| v | <code>string</code> | the name of a vertex |

<a name="DecisionGraph+isTypeAND"></a>
### decisionGraph.isTypeAND(v) ⇒ <code>boolean</code>
is this a type AND vertex (and not a type OR)?

**Kind**: instance method of <code>[DecisionGraph](#DecisionGraph)</code>  
**Returns**: <code>boolean</code> - is this a type AND vertex (and not a type OR)?  

| Param | Type | Description |
| --- | --- | --- |
| v | <code>string</code> | the name of a vertex |

<a name="DecisionGraph+vertices"></a>
### decisionGraph.vertices() ⇒ <code>Array.&lt;string&gt;</code>
get an array of vertex names

**Kind**: instance method of <code>[DecisionGraph](#DecisionGraph)</code>  
**Returns**: <code>Array.&lt;string&gt;</code> - the vertex names in this graph  
<a name="GrammarGraph"></a>
## GrammarGraph
**Kind**: global class  

* [GrammarGraph](#GrammarGraph)
    * [new GrammarGraph(grammar, [seperator], [epsilonSymbol])](#new_GrammarGraph_new)
    * [.vertices()](#GrammarGraph+vertices) ⇒ <code>Array.&lt;string&gt;</code>
    * [.adj(v)](#GrammarGraph+adj) ⇒ <code>Array.&lt;string&gt;</code>
    * [.isTypeAND(v)](#GrammarGraph+isTypeAND) ⇒ <code>boolean</code>
    * [.createGuide(start)](#GrammarGraph+createGuide) ⇒ <code>[GuidedDecisionGraph](#GuidedDecisionGraph)</code>
    * [.createRecognizer(start)](#GrammarGraph+createRecognizer) ⇒ <code>[Recognizer](#Recognizer)</code>

<a name="new_GrammarGraph_new"></a>
### new GrammarGraph(grammar, [seperator], [epsilonSymbol])
creates a new GrammarGraph which can generate guides.


| Param | Type | Default | Description |
| --- | --- | --- | --- |
| grammar | <code>[Grammar](#Grammar)</code> |  | an object representing a grammar. |
| [seperator] | <code>string</code> &#124; <code>RegExp</code> | <code>&quot;/\\s+/&quot;</code> | how tokens will be divided in rules |
| [epsilonSymbol] | <code>string</code> | <code>&quot;&#x27;&#x27;&quot;</code> | Special terminal symbol that indicates this is an end of a construction. Defaults to the empty string. |

<a name="GrammarGraph+vertices"></a>
### grammarGraph.vertices() ⇒ <code>Array.&lt;string&gt;</code>
get an array of vertex names in the graph

**Kind**: instance method of <code>[GrammarGraph](#GrammarGraph)</code>  
**Returns**: <code>Array.&lt;string&gt;</code> - the vertex names in this graph  
**See**: [vertices](#DecisionGraph+vertices)  
<a name="GrammarGraph+adj"></a>
### grammarGraph.adj(v) ⇒ <code>Array.&lt;string&gt;</code>
get an array of all the vertices this vertex points to

**Kind**: instance method of <code>[GrammarGraph](#GrammarGraph)</code>  
**Returns**: <code>Array.&lt;string&gt;</code> - an ordered list of all the vertices that v points to  
**See**: [adj](#DecisionGraph+adj)  

| Param | Type | Description |
| --- | --- | --- |
| v | <code>string</code> | the name of a vertex |

<a name="GrammarGraph+isTypeAND"></a>
### grammarGraph.isTypeAND(v) ⇒ <code>boolean</code>
is this a type AND vertex (and not a type OR)?

**Kind**: instance method of <code>[GrammarGraph](#GrammarGraph)</code>  
**Returns**: <code>boolean</code> - is this a type AND vertex (and not a type OR)?  
**See**: [isTypeAND](#DecisionGraph+isTypeAND)  

| Param | Type | Description |
| --- | --- | --- |
| v | <code>string</code> | the name of a vertex |

<a name="GrammarGraph+createGuide"></a>
### grammarGraph.createGuide(start) ⇒ <code>[GuidedDecisionGraph](#GuidedDecisionGraph)</code>
get a new GuidedDecisionGraph using this decision graph

**Kind**: instance method of <code>[GrammarGraph](#GrammarGraph)</code>  
**Returns**: <code>[GuidedDecisionGraph](#GuidedDecisionGraph)</code> - a new guide from the provided start point  
**See**: [GuidedDecisionGraph](#GuidedDecisionGraph) for the methods available on the Guide  

| Param | Type | Description |
| --- | --- | --- |
| start | <code>string</code> | the name of a vertex in the decision graph from which to start the guided expansion |

<a name="GrammarGraph+createRecognizer"></a>
### grammarGraph.createRecognizer(start) ⇒ <code>[Recognizer](#Recognizer)</code>
Returns a new Recognizer from the given start vertex

**Kind**: instance method of <code>[GrammarGraph](#GrammarGraph)</code>  
**Returns**: <code>[Recognizer](#Recognizer)</code> - a new Recognizer  

| Param | Type | Description |
| --- | --- | --- |
| start | <code>string</code> | the name of a vertex in the decision graph from which to start the recognizer test |

<a name="GuidedDecisionGraph"></a>
## GuidedDecisionGraph
**Kind**: global class  

* [GuidedDecisionGraph](#GuidedDecisionGraph)
    * [new GuidedDecisionGraph(dg, start)](#new_GuidedDecisionGraph_new)
    * [.construction()](#GuidedDecisionGraph+construction) ⇒ <code>Array.&lt;string&gt;</code>
    * [.isComplete()](#GuidedDecisionGraph+isComplete) ⇒ <code>boolean</code>
    * [.choose(terminal)](#GuidedDecisionGraph+choose)
    * [.constructs()](#GuidedDecisionGraph+constructs) ⇒ <code>Array.&lt;string&gt;</code>
    * [.pop()](#GuidedDecisionGraph+pop) ⇒ <code>string</code>
    * [.choices([nDeep])](#GuidedDecisionGraph+choices) ⇒ <code>Array.&lt;string&gt;</code> &#124; <code>[Array.&lt;TreeNode&gt;](#TreeNode)</code>

<a name="new_GuidedDecisionGraph_new"></a>
### new GuidedDecisionGraph(dg, start)
step-by-step construction of a language from a decision graph


| Param | Type | Description |
| --- | --- | --- |
| dg | <code>[DecisionGraph](#DecisionGraph)</code> | a Decision Graph that defines a grammar |
| start | <code>string</code> | the name of a vertex in the decision graph from which to start the guided expansion |

<a name="GuidedDecisionGraph+construction"></a>
### guidedDecisionGraph.construction() ⇒ <code>Array.&lt;string&gt;</code>
the current construction

**Kind**: instance method of <code>[GuidedDecisionGraph](#GuidedDecisionGraph)</code>  
**Returns**: <code>Array.&lt;string&gt;</code> - a terminal symbol chain  
<a name="GuidedDecisionGraph+isComplete"></a>
### guidedDecisionGraph.isComplete() ⇒ <code>boolean</code>
is the current construction a valid, complete construction from the starting
nonterminal? ie, could the construction be haulted at this point? Depending
on the grammar, this may be true even if there are more choices at this point.

**Kind**: instance method of <code>[GuidedDecisionGraph](#GuidedDecisionGraph)</code>  
**Returns**: <code>boolean</code> - is the construction complete  
<a name="GuidedDecisionGraph+choose"></a>
### guidedDecisionGraph.choose(terminal)
adds the given terminal to the construction

**Kind**: instance method of <code>[GuidedDecisionGraph](#GuidedDecisionGraph)</code>  

| Param | Type | Description |
| --- | --- | --- |
| terminal | <code>string</code> &#124; <code>Array.&lt;string&gt;</code> | the name of a terminal vertex in the Decision Graph which is in the current set of possible choices. Or a valid sequence of terminal symbols as an array. |

<a name="GuidedDecisionGraph+constructs"></a>
### guidedDecisionGraph.constructs() ⇒ <code>Array.&lt;string&gt;</code>
get a sorted array of possible construction strings from the current state,
possibly including nonterminals after the next terminal

**Kind**: instance method of <code>[GuidedDecisionGraph](#GuidedDecisionGraph)</code>  
**Returns**: <code>Array.&lt;string&gt;</code> - a list of possible constructions  
**Example**  
```js
// guide is an in-progress GuidedDecisionGraph
guide.construction()   => ['the', 'dog', 'ate']
guide.choices()        => ['', 'the']
guide.constructs()
 => [ 'the dog ate',
      'the dog ate the Noun'
      'the dog ate the Noun RelativeClause' ]
```
<a name="GuidedDecisionGraph+pop"></a>
### guidedDecisionGraph.pop() ⇒ <code>string</code>
pop the last choice off the construction

**Kind**: instance method of <code>[GuidedDecisionGraph](#GuidedDecisionGraph)</code>  
**Returns**: <code>string</code> - the last element of the construction that was
submitted through [choose](#GuidedDecisionGraph+choose)  
**Throws**:

- throws an error if called when construction is empty

<a name="GuidedDecisionGraph+choices"></a>
### guidedDecisionGraph.choices([nDeep]) ⇒ <code>Array.&lt;string&gt;</code> &#124; <code>[Array.&lt;TreeNode&gt;](#TreeNode)</code>
returns all possible next terminals, or an array of nDeep [TreeNodes](#TreeNode)

**Kind**: instance method of <code>[GuidedDecisionGraph](#GuidedDecisionGraph)</code>  
**Returns**: <code>Array.&lt;string&gt;</code> &#124; <code>[Array.&lt;TreeNode&gt;](#TreeNode)</code> - if nDeep=1, an array of terminal symbols (strings),
else an array of [TreeNodes](#TreeNode)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| [nDeep] | <code>number</code> | <code>1</code> | will search for nDeep possible choices |

**Example**  
```js
// guide is an in-progress GuidedDecisionGraph
guide.construction()   => ['the', 'dog', 'ate']
guide.choices()        => ['', 'the']
guide.choices(3)       =>
[ { val: '',
    next: [] },
  { val: 'the',
    next: [ { val: 'squirrel',
             next: [ { val: 'that', next: [] },
                     { val: '',     next: [] } ]
            },
            { val: 'bird',
             next: [ { val: 'that', next: [] },
                     { val: '',     next: [] } ]
            },
            { val: 'cat',
             next: [ { val: 'that', next: [] },
                     { val: '',     next: [] } ]
            },
            { val: 'dog',
             next: [ { val: 'that', next: [] },
                     { val: '',     next: [] } ]
            }
          ]
  }
]
```
<a name="Recognizer"></a>
## Recognizer
**Kind**: global class  

* [Recognizer](#Recognizer)
    * [new Recognizer(dg, start, [seperator])](#new_Recognizer_new)
    * [.isValid(text)](#Recognizer+isValid) ⇒ <code>boolean</code>
    * [.isComplete(text)](#Recognizer+isComplete) ⇒ <code>boolean</code>

<a name="new_Recognizer_new"></a>
### new Recognizer(dg, start, [seperator])
create a Recognizer that can test if text is a valid sentence in a grammar


| Param | Type | Default | Description |
| --- | --- | --- | --- |
| dg | <code>[DecisionGraph](#DecisionGraph)</code> |  | a Decision Graph that defines a grammar |
| start | <code>string</code> |  | the name of a vertex in the decision graph from which to start the test |
| [seperator] | <code>string</code> &#124; <code>RegExp</code> | <code>&quot;/\\s+/&quot;</code> | how tokens will be divided in given text |

<a name="Recognizer+isValid"></a>
### recognizer.isValid(text) ⇒ <code>boolean</code>
is the text a valid in progress sentence in the grammar? Will return true
even if the text is not complete.

**Kind**: instance method of <code>[Recognizer](#Recognizer)</code>  
**Returns**: <code>boolean</code> - is the text valid?  

| Param | Type | Description |
| --- | --- | --- |
| text | <code>string</code> | the text to check |

<a name="Recognizer+isComplete"></a>
### recognizer.isComplete(text) ⇒ <code>boolean</code>
is the text a valid and complete text in the grammar? Will return true
only if the text is complete.

**Kind**: instance method of <code>[Recognizer](#Recognizer)</code>  
**Returns**: <code>boolean</code> - is the text valid and complete?  

| Param | Type | Description |
| --- | --- | --- |
| text | <code>string</code> | the text to check |

<a name="noSelfDefinitions"></a>
## noSelfDefinitions(grammar, returns)
check a grammar for direct self-loops

**Kind**: global function  
**Throws**:

- an error if one definition of a nonterminal is exactly the nonterminal itself


| Param | Type | Description |
| --- | --- | --- |
| grammar | <code>object</code> | the grammar to check |
| returns | <code>true</code> | true if no errors |

<a name="parseGrammar"></a>
## parseGrammar(grammar, [seperator]) ⇒ <code>[DecisionGraph](#DecisionGraph)</code>
parse a grammar given as an object and compile it into a decision graph

**Kind**: global function  
**Returns**: <code>[DecisionGraph](#DecisionGraph)</code> - the grammar converted into a decision graph  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| grammar | <code>object</code> |  | an object representing a grammar |
| [seperator] | <code>string</code> &#124; <code>RegExp</code> | <code>&quot;/\\s+/&quot;</code> | how tokens will be divided in rules |

<a name="reduceGrammar"></a>
## reduceGrammar(grammar, [seperator]) ⇒ <code>object</code>
reduces the rules of a grammar into a one to one form by assigning a name
to all non-terminals. The end result is that each option on a rule with
more than one choice will either be a single AND-rule or a single terminal.

**Kind**: global function  
**Returns**: <code>object</code> - the modified grammar object with newly created rules
as needed. New rules will be given the name of their parent rule
surrounded by underscores and followed by a number.  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| grammar | <code>object</code> |  | an object representing a grammar |
| [seperator] | <code>string</code> &#124; <code>RegExp</code> | <code>&quot;/\\s+/&quot;</code> | how tokens will be divided in rules |

**Example**  
```js
var grammar = {
      NounPhrase: ['the Noun', 'the Noun RelativeClause'],
  RelativeClause: ['that VerbPhrase'],
            Noun: ['dog', 'cat', 'bird']
}

reduceGrammar(grammar)   =>
{
      NounPhrase: ['_NounPhrase_1', '_NounPhrase_2'],
   _NounPhrase_1: ['the Noun'],
   _NounPhrase_2: ['the Noun RelativeClause'],
  RelativeClause: ['that VerbPhrase'],
            Noun: ['dog', 'cat', 'bird']
}
```
<a name="clone"></a>
## clone(obj) ⇒ <code>object</code> &#124; <code>array</code>
helper function to clone a simple object/array made up of primitives.
Will not work if the object or array contains non-primitives.

**Kind**: global function  
**Returns**: <code>object</code> &#124; <code>array</code> - a new clone of the provided object or array  

| Param | Type | Description |
| --- | --- | --- |
| obj | <code>object</code> &#124; <code>array</code> | an object array made up only of primitives |

<a name="SymbolChain"></a>
## SymbolChain : <code>string</code>
a string of one or more symbol names seperated by whitespace or
another user defined seperator (see: seperator param for [GrammarGraph](#GrammarGraph))

**Kind**: global typedef  
**See**: a SymbolChain is used as definitions in [Grammar](#Grammar)  
**Example**  
```js
'dog'                        // just a single symbol, the word 'dog'
'the Noun RelativeClause'    // three symbols
```
<a name="Grammar"></a>
## Grammar : <code>Object</code>
a user defined context-free grammar formatted as an object consisting of key-value pairs,
with each [non-terminal symbol](https://github.com/jrleszcz/grammar-graph#non-terminal-symbols)
pointing to an array of one or more [symbol chains](https://github.com/jrleszcz/grammar-graph#symbol-chains)
choices for this non-terminal.

**Kind**: global typedef  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| symbol | <code>[Array.&lt;SymbolChain&gt;](#SymbolChain)</code> | each element of the array is a possible definition    for this symbol. |

**Example**  
```js
var grammar = {
      Sentence: ['NounPhrase VerbPhrase'],                 // only one definition of 'Sentence'
    NounPhrase: ['the Noun', 'the Noun RelativeClause'],   // two possible definitions of 'NounPhrase'
    VerbPhrase: ['Verb', 'Verb NounPhrase'],
RelativeClause: ['that VerbPhrase'],
          Noun: ['dog', 'cat', 'bird', 'squirrel'],        // four possible definitions of 'Noun'
          Verb: ['befriended', 'loved', 'ate', 'attacked']
}
// non-terminals: Sentence, NounPhrase, VerbPhrase, RelativeClause, Noun, Verb
//     terminals: the, that, dog, cat, bird, squirrel, befriended, loved, ate, attacked
```
<a name="TreeNode"></a>
## TreeNode : <code>object</code>
**Kind**: global typedef  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| val | <code>string</code> | a terminal string |
| next | <code>[Array.&lt;TreeNode&gt;](#TreeNode)</code> | a list of TreeNodes this node links to |

