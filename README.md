# Overview
Klayout code to generate test structures for UV lithography fabrication of 2D materials. 

## Available patterns
- **Tests:**
  - A siemens star for resolution tests
  - Parallel lines
  - A spiral
  - A ruler pattern
  - A vernier ruler
  - A alignment mark using vernier rulers
- **Devices:**
  - Hallbars
  - Lines of increasing length
  - Van der Pouw
 
## Installation 
- Clone the github repo to a folder on your computor.
- Open Klayout
- Press **F5** to enter the macrodevelopment window
- Navigate to the **python tab** in the left menu bar
- Right click in the menu bar and choose **add location**
- Navigate to the folder with the cloned repo and add it
- Click on the file `test_pcell_macros`
- Run the file by pressing F5 or by clicking on on the greeen arrow

## Use 
- To add a PCell from the library, click **Instance** in the main Klayout menu
- Select the library `Nanomade Test Patterns` in the instance tab under Editor Options
- Click the magnifying glass next underneath and select the PCell you want to insert
- Click on the PCell tab under editor options and select the Layer and parameters to use
- Click on the layout to insert the PCell at that position

# PCells
Parametrized Cells (PCells) are a set of classes that can be instantiated from the Klayout menu. They can produce patterns based a set of input parameters. The PCells are defined in the file `test_pcell_macros`. Each PCell is defined as a class in the library `Nanomade Test Patterns` and takes in a set of parameters. The PCells then call the build functions in the `Create` class.


## Align_default
A alignment mark with the default alignment mark from the manual of the uPrinter with a vernier scale added to the sides. The distance between ticks on the vernier scale are givein by the Main Scale Dimension (MSD) and the accuarcy is given by the Least Count (LC). The offset is found by counting the number of ticks from the center tick to the tick where the two scales align, then multiply this number by the LC. 

The parameters used can be found in the following table:

| Obj     	| A [um] 	| B[um] 	| C [um] 	| D [um] 	| MSD [um] 	| LC [um] 	|
|---------	|--------	|-------	|--------	|--------	|----------	|---------	|
| 0.5x    	| 250    	| 2000  	| 1000   	| 40     	| 200      	| 20      	|
| **1x**  	| 140    	| 1000  	| 500    	| 20     	| 100      	| 10      	|
| 2.5x    	| 50     	| 400   	| 200    	| 9      	| 40       	| 4       	|
| 5x      	| 25     	| 200   	| 100    	| 5      	| 20       	| 2       	|
| **10x** 	| 15     	| 100   	| 50     	| 2.2    	| 10       	| 1       	|

### Parameters.
- **Layer 1** - Defines the Layer of the inner alignment mark with the main scale 
- **Layer 2** - Defines the layer of the outer alignment mark with the Vernier scale
- **Objective** - The intended objective of the uprinter 
- **Add vernier** - Bool: Whether to include the vernier scale or not.
- **Label** - Str: An optional label that can be added to the alignmnet mark
- **Label X** - Float: The x coordinate of the label
- **Label Y** - Float: The y coordinate of the label 



## Hallbar 
A parametric design for a hall bar 

### Parameters
- **Layer** - Defines the Layer of the main structure of the hall bar
- **Layer 2** - Defines the layer of the side contacts
- **Side contact gap** - The distance in $\mu m$ between the edge of one side contact and another
- **Side contact length** - Float: The length of the side contacts in $\mu m$
- **Side contact width** - Float: The width of the side contacts in $\mu m$ 
- **Main contact length** - Float: The length in $\mu m$ of the main contacts measured from the end of the side contacts.
- **Main contact width** - Float: The width in $\mu m$ of the main contacts
- **Number of side contacts** - Int: The integer number of side contacts (rounded down to the nearest even number) 

### Build function 
The following is an example of the build function that this PCell calls.
```python
Create.hallbar(shapes, side_contact_gap, side_contact_length, side_contact_width, main_contact_length, main_contact_width, transform=pya.DTrans(0, False, 0, 0), n_side_contacts=4)
```

## Lines
Produces lines of a given height (h) and varying length.


- **Layer (shapes)** - Defines the Layer of the structure
- **Height (h)** - Float: The height of the lines in  $\mu m$
- **Initial width (w0)** - Float: The starting width of the lines in  $\mu m$
- **Change in width (dw)** - Float: The change in the width of the lines with each iteration in  $\mu m$
- **Initail spacing (d0)** - Float: The starting spacing between lines in  $\mu m$
- **Change in spacing (dd)** - Float: The change in the spacing between lines with each iteration in  $\mu m$
- **Number of lines (n)** - Int: The number of lines to produce

### Build function 
The following is an example of the build function that this PCell calls.
```python
Create.lines(shapes, d0, dd ,h , w0 , dw , n)
```

## siemens star
A resolution test that is comprised of n identical triangles spaced equidistant around a central point


### Parameters
- **Layer (shape)** - Defines the Layer
- **Radius (ru)** - Float: The radius of the siemens star in $\mu m$
- **Number of triangles (n)** - int: The number of triangles that the star will comprise, each with a angle of $\frac{\pi}{2n}$. 

### Build function 
The following is an example of the build function that this PCell calls. It produces a siemens star with 32 trangles and a radius of 100um 
```python
Create.siemens_star(shape, n = 32, ru = 100)
```

## Spiral
A spiral that can be used to test undercut when developing. 


### Parameters
- **Layer (shape)** - Defines the Layer
- **Number of points (n)** - The number of points that make up each revolution of the spiral, default = 64. Increae for a more smooth curve
- **Inner radius (inner_r)** - Float: The inner radius of the spiral $\mu m$
- **Outer radius (outer_r)** - Float: The outer radius of the spiral $\mu m$
- **Width (width)** - Float: The width of the spiral arm $\mu m$
- **Spacing (spacing)** - Float: The spacing between each sucessive layer of the spiral arm $\mu m$



## Ruler
A ruler that comprisses a number of teeth/ticks connected by a line. 


### Parameters
- **Layer (shape)** - Defines the Layer
- **Tooth Height (th)** - Float: The height of the teeth/ticks in $\mu m$
- **Tooth Width (tw)** - Float: The width of the teeth/ticks in $\mu m$
- **Line Width (lw)** - Float: The width of the line connecting the teeth/ticks in $\mu m$
- **Length (length)** - Float: The length of the ruler in $\mu m$
- **Spacing (d)** - Float: The distance between teeth/ticks in $\mu m$
- **Major ticks (major)** - int: The number of minor ticks between major ticks, e.g. every 10th tick is taller

### Build function 
The following is an example of the build function that this PCell calls. It produces a ruler with teeth 20um tall by 2um wide spaced 10um appart, that are connected by a 1000um long line that is 2um thick. Every 10th tick (marking 100 um) is taller than the rest.
```python
Create.ruler(th = 10, tw = 2, lw = 2, length = 1000 , d = 10 , major = 10)
```


## Vernier 
Produces a vernier scale that can be use for alignment







## Write_area
Creates a box that corresponds to the dimensions of the write area of the specified objective 


### Parameters
- **Layer** - Defines the Layer
- **Objective** - The objective used



