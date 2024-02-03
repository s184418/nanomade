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

- 
# PCells
Parametrized Cells (PCells) are a set of classes that can be instantiated from the Klayout menu. They can produce patterns based a set of input parameters. 


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
