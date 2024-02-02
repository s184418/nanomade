# Overview
Klayout code to generate test structures for UV lithography fabrication of 2D materials.

***Patterns include:***
- Tests
  - A siemens star for resolution tests
  - Parallel lines
  - A spiral
  - A ruler pattern
  - A vernier ruler
  - A alignment mark using vernier rulers
- Devices:
  - Hallbars
  - Lines of increasing length
  - Van der Pouw 

# PCells
Parametrized Cells (PCells) are a set of classes that can be instantiated from the Klayout menu. They can produce patterns based a set of input parameters.


## Layout







## siemens star
A resolution test that is comprised of n identical triangles spaced equidistant around a central point



## Hallbar 
A parametric design for a hall bar 

- **Layer** - Defines the Layer of the main structure of the hall bar
- **Layer 2** - Defines the layer of the side contacts
- **Side contact gap** - The distance in $\mu m$ between the edge of one side contact and another
- **Side contact length** - The length of the side contacts in $\mu m$
- **Side contact width** - The width of the side contacts in $\mu m$ 
- **Main contact length** - The length in $\mu m$ of the main contacts measured from the end of the side contacts.
- **Main contact width** - The width in $\mu m$ of the main contacts
- **Number of side contacts** - The integer number of side contacts (rounded down to the nearest even number) 

### Build function 

```python
hallbar(shapes, side_contact_gap, side_contact_length, side_contact_width, main_contact_length, main_contact_width, transform=pya.DTrans(0, False, 0, 0), n_side_contacts=4)
```
