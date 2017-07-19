# pyvector - Simple Python Classes for easier SVG generation
The module contains the most important SVG tags as classes with their most used attributes by default to reduce the need of writing SVG markup inside your Python code.

## Installation
`pyvector` is available on PyPI:

        pip install pyvector

## Usage

### Quickstart

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
