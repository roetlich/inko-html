# Inko HTML

A simple HTML library written Inko. This probably isn't production ready, you caution.

## Usage

First import the `Html` and `Attribute` classes:
``` inko
import html::html::Html
import html::html::Attribute

```

Then you can create html elements:

``` inko
let paragraph = Html.p([],[])
```

When you create an Element, you pass two parameters: A list of Attributes, and a list of children. Self-closing (or void) elements (like `<br>`) don't get any children.

With `Html.raw` you can enter whatever raw string you want directly into the html, for example if you want to input a text or a script. This of course means that this library provides no security and you are yourself responsible for avoiding injection attacks. 

Anyways, we can nest these elements to create entire html pages. Here's a more full example:

``` inko
        let paragraph = Html.p([],[Html.raw("Let's code in Inko!"), Html.br([]), Html.raw(":)")])
        let div = Html.div([Attribute.class("welcome text")], [paragraph])

```

And then `div.to_string` will output:

``` html
<div class=\"welcome text\"><p>Let's code in Inko!<br>:)</p></div>
```

Like `p` and `div`, there are bunch of element types predefined. Same goes for attributes, like `class`. But if you need to support custom attributes or custom elements, that is super easy, they are just functions. 

For example, `p` is defined as:

``` inko
    fn pub static p(attributes : Array[Attribute], children : Array[Html]) -> Html {
        return Html.new("p", attributes, children)
    }
```

And self-closing elements like `br` are defined like this:

``` inko
    fn pub static br(attributes : Array[Attribute]) -> Html {
        return Html.self_closing("br", attributes)
    }
```

Of course, if this is still too restrictive, you can always use `Html.raw()` to do whatever you want.



