# CoNLL-U Parser

**CoNLL-U Parser** parses a [CoNLL-U formatted](http://universaldependencies.org/format.html) string into a nested python dictionary. CoNLL-U is often the output of natural language processing tasks.

## Example usage

```python
>>> from conllu.parser import parse, parse_tree
>>> data = """
1   The the DET DT  Definite=Def|PronType=Art   4   det _   _
2   quick   quick   ADJ JJ  Degree=Pos  4   amod    _   _
3   brown   brown   ADJ JJ  Degree=Pos  4   amod    _   _
4   fox fox NOUN    NN  Number=Sing 5   nsubj   _   _
5   jumps   jump    VERB    VBZ Mood=Ind|Number=Sing|Person=3|Tense=Pres|VerbForm=Fin   0   root    _   _
6   over    over    ADP IN  _   9   case    _   _
7   the the DET DT  Definite=Def|PronType=Art   9   det _   _
8   lazy    lazy    ADJ JJ  Degree=Pos  9   amod    _   _
9   dog dog NOUN    NN  Number=Sing 5   nmod    _   SpaceAfter=No
10  .   .   PUNCT   .   _   5   punct   _   _

"""

>>> # GitHub replaces tab characters with spaces so for this code to be copy-pastable
>>> # I've added the following two lines. You don't need them in your code
>>> import re
>>> data = re.sub(r" +", r"\t", data)

>>> parse(data)
[[
    OrderedDict([
        ('id', 1),
        ('form', 'The'),
        ('lemma', 'the'),
        ('upostag', 'DET'),
        ('xpostag', 'DT'),
        ('feats', OrderedDict([('Definite', 'Def'), ('PronType', 'Art')])),
        ('head', 4),
        ('deprel', 'det'),
        ('deps', None),
        ('misc', None)
    ]),
    OrderedDict([
        ('id', 2),
        ('form', 'quick'),
        ('lemma', 'quick'),
        ('upostag', 'ADJ'),
        ('xpostag', 'JJ'),
        ('feats', OrderedDict([('Degree', 'Pos')])),
        ('head', 4),
        ('deprel', 'amod'),
        ('deps', None),
        ('misc', None)
    ]),
    ...
    OrderedDict([
        ('id', 10),
        ('form', '.'),
        ('lemma', '.'),
        ('upostag', 'PUNCT'),
        ('xpostag', '.'),
        ('feats', None),
        ('head', 5),
        ('deprel', 'punct'),
        ('deps', None),
        ('misc', None)
    ])
]]

>>> parse_tree(data)
[[
    TreeNode(
        data=OrderedDict([
            ('id', 5),
            ('form', 'jumps'),
            ('lemma', 'jump'),
            ('upostag', 'VERB'),
            ('xpostag', 'VBZ'),
            ('feats', OrderedDict([
                ('Mood', 'Ind'),
                ('Number', 'Sing'),
                ('Person', '3'),
                ('Tense', 'Pres'),
                ('VerbForm', 'Fin')
            ])),
            ('head', 0),
            ('deprel', 'root'),
            ('deps', None),
            ('misc', None)]),
        children=[
            TreeNode(
                data=OrderedDict([
                    ('id', 4),
                    ('form', 'fox'),
                    ('lemma', 'fox'),
                    ('upostag', 'NOUN'),
                    ('xpostag', 'NN'),
                    ('feats', OrderedDict([('Number', 'Sing')])),
                    ('head', 5),
                    ('deprel', 'nsubj'),
                    ('deps', None),
                    ('misc', None)
                ]),
                children=[
                    TreeNode(
                        data=OrderedDict([
                            ('id', 1),
                            ('form', 'The'),
                            ('lemma', 'the'),
                            ('upostag', 'DET'),
                            ('xpostag', 'DT'),
                            ('feats', OrderedDict([('Definite', 'Def'), ('PronType', 'Art')])),
                            ('head', 4),
                            ('deprel', 'det'),
                            ('deps', None),
                            ('misc', None)
                        ]),
                        children=[]
                    ),
                    TreeNode(
                        data=OrderedDict([
                            ('id', 2),
                            ('form', 'quick'),
                            ('lemma', 'quick'),
                            ('upostag', 'ADJ'),
                            ('xpostag', 'JJ'),
                            ('feats', OrderedDict([('Degree', 'Pos')])),
                            ('head', 4),
                            ('deprel', 'amod'),
                            ('deps', None),
                            ('misc', None)
                        ]),
                        children=[]
                    ),
                    TreeNode(
                        data=OrderedDict([
                            ('id', 3),
                            ('form', 'brown'),
                            ('lemma', 'brown'),
                            ('upostag', 'ADJ'),
                            ('xpostag', 'JJ'),
                            ('feats', OrderedDict([('Degree', 'Pos')])),
                            ('head', 4),
                            ('deprel', 'amod'),
                            ('deps', None),
                            ('misc', None)
                        ]),
                        children=[]
                    )
                ]
            ),
            ...
            TreeNode(
                data=OrderedDict([
                    ('id', 10),
                    ('form', '.'),
                    ('lemma', '.'),
                    ('upostag', 'PUNCT'),
                    ('xpostag', '.'),
                    ('feats', None),
                    ('head', 5),
                    ('deprel', 'punct'),
                    ('deps', None),
                    ('misc', None)
                ]),
                children=[]
            )
        ]
    )
]]

```

NOTE: TreeNode is a namedtuple so you can loop over it as a normal tuple.

You can read about the CoNLL-U format at the [Universial Dependencies project](http://universaldependencies.org/format.html).

## Why should you use conllu?

- It's simple. ~50 lines of code (including whitespace).
- It has no dependencies

## Installation

```bash
pip install conllu
```

## Develop locally and run the tests

```bash
git clone git@github.com:EmilStenstrom/conllu.git
cd conllu
python setup.py test
```
