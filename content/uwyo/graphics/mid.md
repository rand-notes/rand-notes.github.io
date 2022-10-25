---
date: 2021-09-02
title: Midterm
url: uwyo/graphics/0
---

| Local space
| | Model Matrix
| World space
| | View matrix
| View space 
| | projection matrix
| Clip space
| Screen space


gluOrtho2D - create world window
gluOrtho2D — define a 2D orthographic projection matrix
glLoadIdentity replaces the current matrix with the identity matrix

glViewport(40,60,360,240)

Normals - describe the orientation of a surface of a geometric object at a point on that surfac
normal vector - perpendicular to the surface

# Window-to-Viewport Mapping

Based on formula that produces a point (sx,sy) in the screen-window coordinates for any given point (x,y) in the world coordinates


# Modeling Task

- To create and/or use Geometric objects
- Space where geometric objects are described as is called the world coordinates

# Viewing Task

- To size and position the pictures of those geometric objects on the display
- Space where the viewport displays output from mappings in screen coordinates


Modelview matrix is composed of the scene transformations, M, and the camera transformations, V.

Graphic pipeline:

Modelview matrix -> projection matrix -> perspective division -> viewport matrix -> |window
coordinates|

# Projection Transformation

View Volume
- Parallel
- Perspective
- isometric
Types of Projection
- Parallel (orthographic)
- perspective
Important to Control
- Projection type
- Field of view and image aspect ratio
- Near and far clipping planes


# Parallel (Orthographic) projection

No foreshortening effect
- Distance from camera does not matter
- Objects are same size no matter what

The center of projection is at infinity

Projection calculation
- Just choose to equal the z coordinates

# Field of View
- Determine how much of the world is going to be “seen”
- Larger field of view = smaller object projection size

# Camera

- The camera has an eye (or view reference point VRP) at some point in space
- Its view volume is a portion of a pyramid, whose apex is at the eye
- The straight line from a point P to the eye is called the projector of P. (All projectors of a point meet at the eye.)
- The axis of the view volume is called the view plane normal, or VPN
- The opening of the pyramid is set by the viewangle
- Three planes are defined perpendicular to the VPN - near plane, the view plane, and the far plane
- The windows have an aspect ratio which can be set in a program
- OpenGL clips points of the scene lying outside the view volume (view frustum)
- Points P inside the view volume are projected onto the view plane to a corresponding point P
- Finally, the image formed on the view plane is mapped into the viewport, and becomes visible on the display device


# Points

- have position
- Do not have length and direction (relative to a coordinate system)

# Vectors

- have length and direction
- Does not have position (relative to coordinate system)
- can be moved anywhere
- A vector is displacement from one point to another

- displacement: the moving of something from its place or position.


# Scalar
- size only (a number)


# Basics of Points and Vectors

- All points and vectors are defined relative to some coordinate system.

example: 2d coordinate system

# Vector Representations

v = (1, 2, 3) is a row vector
v = (1, 2, 3)^T is a column vector

Subtracting c from a is equivalent to adding a and -c.


The magnitude (length, size) of n-vector w is written |w|.

`|w| = sqrt(w_1^2 + w_2^2 + ...)`

# OpenGL Routines

-glScaled (sx, sy, sz);
2D: sz = 1.0

-glTranslated (tx, ty, tz);
2D: tz = 0.0

-glRotated (angle, ux, uy, uz);
2D: ux = uy = 0.0; uz = 1.0

# Transformations

Transformations change 2D or 3D points and vectors, or change coordinate systems

An **object transformation** alters the coordinates of each point on the object according to the same rule, leaving the underlying coordinate system fixed.

A **coordinate transformation** defines a new coordinate system in terms of the
old one, then represents all of the object’s points in this new system

A coordinate frame consists of:
 - a point O, called the origin
 - and some mutually perpendicular vectors that serve as the axes of the coordinate frame
- Standard Unit Vectors are Used: The unit vectors are orthogonal
- A unit vector has magnitude |v| = 1


# Affine Transformations

Successive affine transformations can be combined into a single overall affine transformation.

affine transformation is a geometric transformation that preserves lines and parallelism (but not necessarily distances and angles). 

Matrix M form of the affine trans for 2D
```
(Qx)  (m m m)(P) 
(Qy) =(m m m)(P)
(1 )  (0 0 1)(1)
```

M is post multiply
M^t is pre multiply


# 3-D Affine Transformations

The matrix representing a transformation is now 4 x 4


# Perspective Matrix

public static Matrix4x4 Perspective(fov, aspect, znear, zfar)

- Set glmatrix mode to GL_Projection
- For perspective projection use: gluPerspective
or 
- glFrustrum(left, right, bottom, top, new, far);
- For orthographic projection, use: glOrtho


# Setting the View Volume

- Define a look point as a point of particular interest in the scene, and together the
two points eye and look define VPN as eye-look
- This is later normalized to become the vector n, which is central in specifying the
camera properly.
- VPN points from look to eye.
- 

# Projection Plane
- Projection plane called the view plane in computer graphics
- Is defined by a point called view reference point (VRP) and a normal (a vector perpendicular to the plane) called view plane normal (VPN).

# Viewing Transformation

- gluLookAt fills V part of modelview matrix
- Modelview Matrix: Combination of modeling matrix M and Camera transforms V


# gluLookAt

gluLookAt takes the points eye and look, and the vector up

//TODO construct look at

# Camera with Arbitrary Orientation and Position

- Position is easy to describe, but orientation is difficult.
- We specify orientation using the flying terms: pitch, heading, yaw, and roll.


# Flying the Camera through a Scene

- The user can fly the camera through a scene interactively by pressing keys or
	clicking the mouse.

# Flying the Camera through a Scene

There are six degrees of freedom for adjusting a camera:
- it can fly in three dimensions
- it can be rotated about any of three coordinate axes
- We first develop the slide() function


# Polygonal Meshes

A polygonal mesh is a collection of polygons (faces) that approximate the surface of
a 3D object.

# 3D Modeling

Polygonal meshes capture the shape of complex 3D objects in simple data structures
- Platonic solids, the Buckyball, geodesic domes, prisms
- Extruded or swept shapes, and surfaces of revolution
- Solids with smoothly curved surfaces

Animated Particle systems:
– Each particle responds to conditions.
– Position, a velocity, and perhaps a color, lifetime, size, degree of transparency, and shape.
– Randomly generated

# Polygonal Meshes

- Polygons are easy to represent (by a sequence of vertices) and transform
- They have simple properties (a single normal vector, a well-defined inside and
	outside, etc.)
- They are easy to draw
- Meshes are a standard way of representing 3D objects in graphics
- A mesh can approximate the surface to any degree of accuracy by making the mesh finer or coarser

Meshes can model both solid shapes and thin skins.
- The object is solid if the polygonal faces fit together to enclose space.
– the faces fit together without enclosing space

# Polygonal Meshes in OpenGL

- A polygonal mesh is described by a list of polygons, along with information about the direction in which each polygon is facing.
- If the mesh represents a solid, each face has an inside and an outside relative to the rest of the mesh
- In such a case, the directional information is often simply the outward pointing normal vector to the plane of the face used in the shading process.

# Polygonal Meshes: Normal Vector

- The normal direction to a face determines its brightness
- For some objects, we associate a normal vector to each vertex of a face rather
	than one vector to an entire face.
- We use meshes, which represent objects with smoothly curved faces such as a sphere
	or cylinder
- smooth-underlying surface

# Polygonal meshes 
- For the smoothly curved surface of the cylinder, both vertex V1 of face F1 and vertex V2 on face F2 use the same normal n, the vector perpendicular to the underlying smooth surface. 
- basically: we we put e.g. hexagon around circle, and taking normals for circle from hexagon


# Defining a Polygonal Mesh

- A mesh consists of 3 lists: the vertices of the mesh, the outside normal at each vertex, and the faces of the mesh.
- It has a square floor one unit on a side.


# Defining a Polygonal Mesh

- The vertex list reports the locations of the distinct vertices in the mesh
- The list of normals reports the directions of the distinct normal vectors that occur in the model
- The face list indexes into the vertex and normal lists
- The list of vertices for a face begins with any vertex in the face, and then
proceeds around the face vertex by vertex until a complete circuit has been made.

There are two ways to traverse a polygon:
 - clockwise
 - counter-clockwise


Convention: Traverse the polygon counterclockwise as seen from outside the object
- Using this order, if you traverse around the face by walking from vertex to vertex, the inside of the face is on your left.
- Using the convention allows algorithms to distinguish with ease the front from the back of a face.
- If we use an underlying smooth surface, such as a cylinder, normals are computed for that surface.

# Properties of Meshes

- A mesh is convex if the line connecting any two interior points is entirely inside the mesh.
- Exterior connecting lines are shown for non-convex objects below (step and torus).
- A closed mesh represents a solid object (which encloses a volume)
- A mesh is connected if there is an unbroken path along the edges of the mesh between any two vertices.
- A mesh is simple if it has no holes. Example: a sphere is simple; a torus is not.
- A mesh is planar if every face is a plane polygon. Triangular meshes are frequently used to enforce planarity. 

# Platonic Solids

All the faces are identical and each is a regular polygon.



# Calculating Normals

`m = (V1 - V2) x (V3 - V2)`


# Newell's Method for Normals

- Given N vertices, define: next(i) = ni = (i+1) mod N.
- Traverse the vertices for the face in counter-clockwise order from the outside
- The normal given by the values on the next slide points to the outside (front) of the face


# Extruded Shapes

- A large class of shapes can be generated by extruding or sweeping a 2d shape through space.
- In addition, surfaces of revolution can also be approximated by extrusion of a
	polygon once we slightly broaden the definition of extrusion.
- Prism: formed by sweeping the arrow along a straight line.


# Prisms

- A prism is formed by moving a regular polygon along a straight line.
- When the line is perpendicular to the polygon, the prism is a right prism

# Extruded Shapes

- Base has vertices (xi, yi, 0) and top has vertices (xi, yi, H).
- Each vertex (xi, yi, H) on the top is connected to corresponding vertex (xi, yi, 0) on the base
- If the polygon has n sides, then
 - n vertical sides of the prism
 - a top side (cap) 
 - a bottom side (base), or n+2 faces altogether


- The normals for the prism are the face normals.
- These may be obtained using the Newell method, and the normal list for the prism constructed



# Arrays of Extruded Prisms

OpenGL can reliably draw only convex
polygons. For non-convex prisms, stack the
parts.

# Vertex List for the Prism

- Suppose the prism's base is a polygon with N vertices (xi, yi).
- We number the vertices of the base 0, . . . , N-1 and those of the cap N, . . ., 2N -1, so that an edge joins vertices i and i + N
- The vertex list is then easily constructed to contain the points (xi, yi, 0) and (xi, yi, H), for i = 0, 1, ..., N-1.


# Face List for the Prism

We first make the side faces and then add the cap and base

