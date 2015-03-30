#CSS Guidelines
This is the guide for how to write great and effecient CSS. Here we will try to
lay some ground rules to we should stick to and also explain some of the
decisions we made when when writing CSS. Maybe you have heard about some of the
principles described in here, cause we are not reinventing the wheel here, at
least not in CSS guidelines.

##BEM Syntax
What is BEM syntax? Simply put, BEM is an abbreviation made of three words - 
Block, Element and Modifier. The three words represent the key ideas behind
BEM syntax. In some way, you can think of BEM as a way of OOP programming used
in other programming languages, but this one is great for CSS. 

###What is BEM?
####Block
Is an independent entity - basic 'building block' of a web application. Search 
bar, main menu or side bar are perfect examples of such blocks. Of course, we 
can think of many other blocks, but just to give ou a hint of what we are 
talking about that is enough. Let's get deeper. Blocks can actually contain 
other blocks. Side bar block can contain some calendar widget block for example.

####Element
Is a part of block that performs a certain function. Be aware, that elements 
have meaning only inside blocks, they are context-dependent. A nice example of 
element would be a input field or a submit button of search form.

####Modifier
Is a variation of the block or element. It comes handy when you are trying to 
reuse the same building block but present in a slightly different way. Main 
menu for example can be presented by a dropdown menu, navigation pills, tabs 
and many more.

###Naming conventions
We now know what we will be using in BEM syntax, let's see how we will be using 
it. We will be sticking to some basic rules here to avoid common errors when 
giving names to our blocks and elements.

1. We must assign our block/element a unique `class` name.
2. We do not use ordinary HTML element selectors.
3. Avoid using cascading selectors.
4. Using elements `id` attribute for CSS rules is highly discouraged.

Examples of such names can be:
```
menu
sidebar
clock-widget
calendar-widget
...
```

Names as we just describe make a nice solution for blocks (independent entities/
building blocks). But what about elements (smaller stuff inside blocks)? As 
indicated that elements are inside the blocks so CSS class names for elements 
must consist of `block name` following with the `element name` to indicate that 
they are part of some block. When concatenating these two parts we will use two 
underscores `__` to designate that this is an element of a block. Two 
underscores are used to distinguish BEM from the most common used naming 
conventions with hyphens `-` or single underscores `_` which take care of 
multiple word names. This way we can distinguish what is element of block or 
what is a multiple word name.

Example of some elements inside `menu` block:
```
menu__item
menu__show
menu__hide
...
```
Elements can be nested further as elements of elements.

Example of nested elements on 'menu__item' element:
```
menu__item__image
menu__item__title
menu__item__caret
...
```

Please, bare in mind that it is highly discouraged to go deeper than three 
levels of hierarchy with such naming to support readability of the CSS rules. 
If you find yourselves having name like 
`menu__item__carousel__navigation__left__icon`, that might be a time to rethink 
naming and structure of the whole block/element.

You might ask yourselves, why are we going for such naming conventions, can we 
just nest the elements inside CSS? Of course we can nest elements and 
subelements inside blocks. The reason is simple, performance. Every level of 
CSS selectors nesting adds unnecessary performance issues to the browser. We 
are not gonna explain how it works, you should just trust us.

Okey! Let's get to the modifiers. As we described it, modifier stands for 
different presentation of the same content. The different presentation could 
have the meaning of just an inverted colours for the element, but also 
completely different structure. A nice example would be having the same menu in 
the `header` and also `footer` HTML tags, but the structure will different. One 
will use 'ul' and 'li', other one can use 'nav pills' or whatever else.

Modifier can be used on blocks or elements, but it is better suited for the 
block use.

The `modifier name` appears at the end of the `block name` or `element name`. 
The `modifier name` is concatenated with the rest of the name with double dash 
symbol `--`. Again, the choice has been made due to the different naming 
conventions.

Example of modifiers used on `menu` block:
```
menu
menu--header
menu--side-bar
menu--footer
...
```

Another example used on `menu__item` element:
```
menu__item
menu__item--inverted
menu__item--featured
menu__item--sticky
...
```

The possibilities here are endless, but we strongly encourage use of clever 
mind and not to overdo it.