# pyvector - Simple Python Classes for easier SVG generation
The module contains the most important SVG tags as classes with their most used attributes by default to reduce the need of writing SVG markup inside your Python code.


## Installation
`pyvector` is available on [PyPI](https://pypi.python.org/pypi/pyvector/):

        pip install pyvector


## Usage

### Quickstart
For the first steps, let's draw a purple `rect` in a `g`:

        from pyvector import SVG, Group, Rect
        svg = SVG()
        g = Group()
        svg.add(g)
        r = Rect(x=1, y=1, width=100, height=20)
        r.style.fill = '#FF00FF'
        g.add(r)
        svg.auto_resize()
        print(svg)

Output:

        <?xml version="1.0" encoding="UTF-8"?>
        <svg viewBox="1 1 100 20" xmlns="http://www.w3.org/2000/svg">
        <g>
        <rect x="1" width="100" y="1" height="20" style="fill:#FF00FF;"/>
        </g>
        </svg>

Result:

![rect.svg](rect.png)


### Classes
The main focus of this package is to provide auxiliary classes to write legible SVG code from within Python.
Thus, the following classes simply represent the most used SVG tags with their inherent properties for code completion in most IDEs.

- *SVG*: Top level container class for the whole canvas.
- *Group*: `g` container class for grouping elements.
- *Text*: Stores text in the `.text` property.
- *Rect*: Draws rectangles.
- *Circle*: Draws circles.
- *Ellipse*: Draws ellipses.
- *Line*: Draws a line from `x1,y1` to `x2,y2`.


### Transformations
All Elements can be transformed by `.translate()`, `.scale()` or `.rotate()`.
By default these transformations are simply passed to the `transform` property of the respective element.
By invoking `.apply_transform()` all non-rotational transformations are applied to the element (and its children, in the case of containers) directly.

**Beware: In the current implementation only a few transformations are implemented and these are most likely not even correct. Just don't use** `.apply_transform()` **for now!**


### Styling
Each element has a `style` attribute, which in turn can have further attributes that correspond to the `style="fill: #F00; stroke: #555;"` attribute in SVG tags.

Alternatively SVG let's you put style attributes directly into the SVG element `<rect fill="#F00" stroke="#555">`.
This can be achieved by liberally adding properties to an element's instance on the fly.
Note, that attributes with hyphens have to be written with an underscore in python (to work around the minus sign).
All underscores in attribute names will be replaced by hyphens during rendering.
Not sure, who ever thought `font`*minus*`size` made for a good attribute name.

The third option is to provide styling through a style sheet in CSS by setting the `SVG.CSS` property which is global to the `SVG` class.
To style individual elements by `.class` selection, elements have to be given a class name by setting the `.class_name` property.
This is a workaround for the fact that python syntax does not allow you to set the `object.class` property.
So `tag.class_name = 'grid'` will be used as `<tag class="grid">` during rendering.


### Viewbox
`SVG` tries to calculate and set the `viewBox` attribute automatically so, all elements inside are visible in the resulting image when `.auto_resize()` is called.
So do this just before rendering to see the proper image in most preview programs (that don't let you zoom out).


### Troubleshooting
If you find a bug, gross inconsistencies or just have a question regarding this project please contact me via github or open an issue. I would love some feedback on this package.
