# Plotter

Plotter project created with vue  
A production copy of this project is available to view here: https://cjf-plotter.netlify.com/

## Build instructions  
* cd to project folder  
* run `npm install` to install required modules  
* run `npm run serve` to start a development server (default http://localhost:8080)

## Usage instructions
* Type inputs into the text area in order for the plotter to draw objects onto the SVG object.
* Initial commands:  
    * Rectangle: `R <X Coordinate> <Y Coordinate> <Width> <Height>`
    * Circle: `<CX Coordinate> <CY Coordinate> <Radius>`
    * Polygon: `<X1,Y1> <X2,Y2> <X3,Y3> ..... <Xn,Yn>`
* Bonus commands:
    * Ellipse: `E <CX Coordinate> <CY Coordinate> <X Radius> <Y Radius>`  
    Draws an ellipse with center at the provided CX, CY coordinates, with X & Y radius as provided.
    * Line: `L <X1 Coordinate> <Y1 Coordinate> <X2 Coordinate> <Y2 Coordinate> <Stroke Width>`  
    Draws a single line with starting vertex at X1 & Y1 coordinate provided, and ending vertex at X2 & Y2 coordinate provided, with a stroke width as provided.
    * Polyline: `PL <X1,Y1> <X2,Y2> <X3,Y3> ..... <Xn,Yn>`  
    Draws a continuous polyline with segments joined by endpoints in the order provided by each coordinate.  

Example commands are provided on the page. For instance, the following command will draw a filled star: `p 81,186 125,50 169,186 54,102 196,102`