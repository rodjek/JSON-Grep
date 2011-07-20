###Installation:###

    gem install jgrep

###JGrep binary usage:###

    jgrep "foo.bar=1" foo.json
        or
    cat "foo.json" | jgrep "foo.bar=1"

###Flags:###
    -s [document field] : Greps the json and only returns the value of the field specified
    -f                  : Display ugly json

###Statements:###

    A statement is defined as some value in a json document compared to another value.
    Available comparison operators are '=', '<', '>', '<=', '>='

    Example: foo.bar=1

###Complex statements:###

    Statements can be combined to form logical sentences. Order of precedence can be set with '(' and ')'
    Available logical operaters are 'and', 'or', '!'.

    Example: !(foo.bar=1) and (foo=bar)

###In document comparison:###

    If a document contains an array, the '[' and ']' operators can be used to define a comparison where
    statements are checked for truth on a per element basis.

    Example: [bar1=1 and bar2=2]

    on [{"foo":[{"bar1":1}, {"bar2":2}]},{"foo":[{"bar1":0}, {"bar2":0}]}]

    will return

    {foo:[bar1:1,bar2:2]}

**Note**: In document comparison cannot be nested.

###JGrep Gem usage:###

    _require 'jgrep'_

    _json = File.read("yourfile.json")_
    _expression = "foo=1 or bar=1"_

    _JGrep::jgrep(json, expression)_