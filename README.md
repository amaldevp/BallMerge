Preliminary implementation of the Eurographics 2024 paper titled "BallMerge: High-quality Fast Surface Reconstruction via Voronoi Balls" - a Delaunay-based Surface reconstruction algorithm.


This is a licensed software and is only for research purposes. If you use, please cite it as follows: "Parakkat AD, Ohrhallinger S, Eisemann E, Memari P. BallMerge: High-quality Fast Surface Reconstruction via Voronoi Balls. In Computer Graphics Forum 2024"

The code uses CGAL and happily.h (included in the repository and is not a property of the authors), and is successfully tested on Mac and Ubuntu.

For license and questions, please contact adparakkat@gmail.com


The source codes (both automatic and parametric versions). Inside the parametric version, it has both the local and global ballmerge codes combined.

The objective of the automatic algorithm is to reconstruct watertight surfaces automatically - and it works well for clean point clouds (it can handle small holes). To run the code, "make" inside the automatic folder and just use "./Group filename", and it will create the PLY file (it uses happly.h).

The algorithm needs a seed tetrahedron to start with. We chose the tetrahedron with the largest circumradius and is part of the Convex hull. But this might not always be enough (we can use some better criteria for the seed tetrahedron - the only thing is that this seed should lie inside the surface).



The local algorithm is designed for open surfaces or scans with outliers (up to a decent level). It also works for clean scans (but might have small missing triangles). Whereas the global algorithm is the same as the automatic algorithm and can be run in case, you need quick output and is fine with tuning the parameter.

To run the local and global variants, just open and run "make" inside the parametric folder.

To execute the code, the command is as follows: "./Group filename IR_Parameter global(1)/local(0) [optional pruning_parameter]"

For example, "./Group 366_kitten_final.xyz 1.85 1" will run the global algorithm with parameter 1.85. And "./Group 599_cinghiale100000.xyz 1.92 1" will run the global algorithm with parameter 1.92.

This global variant creates two PLY files (one of them will be the surface that we need).

For local ballmerge: "./Group aphrodite.xyz 1.85 0" will give a good result and ignore outliers.

Local ballmerge might result in unnecessary long triangles or sometimes result in too many missing triangles. Both these cases can be handled by altering the last optional parameter (which is, by default, 200 - we didn't normalize it). If you feel the result misses many required triangles, then decrease the value; otherwise, increase it.

For example, "./Group 599_cinghiale100000.xyz 1.92 0" will be missing many triangles, so give a smaller value than 200 "./Group 599_cinghiale100000.xyz 1.92 0 100" will create the desired result. The same for kitten, "./Group 366_kitten_final.xyz 1.85 0 80" will give a decent result.



For more details, please have a look at our paper - https://hal.science/hal-04457247



Disclaimer: The author(s) of this software shall not be held responsible or liable for any errors, inaccuracies, or consequences arising from the use or misuse of the software/documentation. Users are advised to use the software/documentation at their own risk and to exercise due diligence in verifying its accuracy and suitability for their intended purposes.
