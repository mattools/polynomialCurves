# Polynomial Curves

Manipulation of smooth curves with Matlab, by considering a polynomial for each coordinate.

Requires the MatGeom toolbox.

Please note that the project is no longer maintained.

## Installation

First download or clone the project. 

To install the library, you simply need to add the path to the main directory of the library :

    >> addPath('basePath/polynomialCurves2d');


## Quick example

The package was originally designed to simplify and smooth the display of skeletons as obtained from binary images.
Let us start by computing the skeleton of a binary image (image is provided with Matlab).
  
    % Fit a set of curves to a binary skeleton
    img = imread('circles.png');
    
    % compute skeleton, and ensure one-pixel thickness
    skel = bwmorph(img, 'skel', 'Inf');
    skel = bwmorph(skel, 'shrink');
    figure; imshow(skel==0)

![Skeleton of a binary image](https://github.com/mattools/polynomialCurves/blob/main/demos/circles_skeleton.png)

From the skeleton image, it is possible to compute a series of polynomial curves.
The result is given as a cell array, each cell containing the data for a single curve.

    % compute coeff of each individual branch
    coeffs = polynomialCurveSetFit(skel, 2);
    
    % Display segmented image 
    figure; imshow(~img); hold on;
    
    % overlay curves
    for i = 1:length(coeffs)
        hc = drawPolynomialCurve([0 1], coeffs{i});
        set(hc, 'linewidth', 2, 'color', 'g');
    end

![Overlay of skeleton curves over original image](https://github.com/mattools/polynomialCurves/blob/main/demos/circles_skeletonCurves.png)

