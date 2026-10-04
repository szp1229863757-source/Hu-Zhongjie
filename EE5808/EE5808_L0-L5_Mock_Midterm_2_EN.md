# EE5808 Topics in Computer Graphics

## Mock Midterm 2

**Scope:** L0–L5 (Weeks 1–5, Test 1 style)

**Closed book. 120 minutes. Full mark: 100.**

This is a revision paper, not the official test. The numbers and the scenes are new: they are not the questions from Mock Midterm 1 or from the outline practice set. Solutions are in a separate file. Finish the paper before you open that file.

| | |
|---|---|
| Name | |
| Student ID | |
| Score | / 100 |

### Instructions

1. Answer in English. Write every matrix as a 4×4 homogeneous matrix. Keep exact values such as √2 and 1/√2.
2. Show the main steps. A bare final number whose working is wrong does not receive full marks.
3. OpenGL angles are in degrees. The C functions `cos`, `sin`, and `pow` use radians.
4. For every true/false item, write **T** or **F** and give a one-line reason.
5. Points are column vectors and stand on the right of a matrix. A composite acts from right to left.
6. Use the lecture conventions. In particular, for `gluLookAt`, VPN = eye − look-at point, and the camera looks along −Z.

| Section | Content | Marks |
|---|---|---|
| A | True / false, with a one-line reason | 20 |
| B | Short answers | 20 |
| C | Calculations | 40 |
| D | Code | 20 |
| **Total** | | **100** |

---

## Section A. True or false, with a one-line reason

2 marks each, 20 marks.

**A1.** `|A × B| = |A| |B| cos α`, where α is the angle between A and B.

**A2.** If a 4×4 matrix contains both a rotation and a translation, its inverse is still equal to its transpose.

**A3.** Seen from outside the solid, a hidden back face should have its vertices listed counter-clockwise.

**A4.** The camera axis is `Xvc = |VPN × VUP|`.

**A5.** By default, `gluCylinder` lies along +Z, with its base at z = 0 and its top at z = height.

**A6.** The axis of `glRotatef(theta, x, y, z)` always passes through the current origin.

**A7.** `glScalef(-1, 1, 1)` mirrors a left wing onto a right wing and leaves a counter-clockwise vertex order counter-clockwise.

**A8.** Replacing a projection direction Vp by −Vp changes the foreshortening ratio and changes xp and yp.

**A9.** An isometric projection is an orthographic projection whose direction is parallel to (±1, ±1, ±1).

**A10.** In the lecture perspective matrix, with the PRP at the VC origin, the fourth row is `(0, 0, 0, 1)`. Dividing by W is optional.

---

## Section B. Short answers

5 marks each, 20 marks.

**B1.** Homogeneous coordinates and a second camera.

(a) Convert `(6, −3, 9, −3)` to a Euclidean point. Why is W = 0 not allowed for an ordinary point?

(b) A second camera C2 has its origin at `(4, 0, 0)` in camera C1, and the two cameras have parallel axes. Write `M_{C2 ← WC}` in terms of `M_{C1 ← WC}`. Which image of the C1-point `(4, 0, 0)` checks the sign?

**B2.** Planes, tables, and inside / outside tests.

(a) How many numbers in `aX + bY + cZ + d = 0` are independent? If `(a, b, c)` is a unit normal, what is `−d`?

(b) Give the two legal ways to store one face. Name two quantities that belong in the attribute table.

(c) State the half-space test for a point inside a convex solid. What must be done instead for a concave solid, and how is a grazing intersection handled?

**B3.** One matrix, two frames.

(a) State the two meanings of a single 4×4 matrix, and write the symbol that takes a point from frame i to frame j.

(b) Treat frame 2 as an object. In its own coordinates it is scaled by 2 about the origin and placed on frame 3. There is no translation, and the axes stay parallel. Write `M_{3 ← 2}`. Also expand `(T S)^{−1}`.

(c) A camera rotates by +60° about its own +Z axis. Write `M_new` in terms of `M_old`. Which side is the new factor on, and which lecture rule fixes the sign?

**B4.** The matrix stack, four wheels, and shear.

(a) What does `glPopMatrix` restore? Contrast a push/pop pair written inside one part with a push/pop pair written at a branch of the graph.

(b) A car has width `w` along X and length `l` along Y. The body centre is the origin. Using successive `glTranslatef` calls only, as in the lecture, place the right-front wheel, then the left-front, then the left-rear, then the right-rear. Give the world position of the right-rear wheel, and say in one sentence why a push/pop pair is safer if another part is inserted between two wheels.

(c) Write the 4×4 matrix of the shear `X' = X + 2Z`, `Y' = Y − Z`, `Z' = Z`. Give the 16-float column-major array passed to `glMultMatrixf`. What does every affine transform do to parallel lines?

---

## Section C. Calculations

40 marks. Keep exact values.

**C1.** (8 marks) Let `A = (1, 2, 2)` and `B = (2, −1, 2)`.

(a) Compute `A · B`, `|A|`, `|B|`, and `cos α`. (2 marks)

(b) Compute `A × B`, and show that the result is perpendicular to both A and B. (3 marks)

(c) Let N be the unit vector of A and let L be the unit vector of B. Take `kd = 1/4` and `Il = 8`. Find `I_diff`. What is `I_diff` if N is replaced by `−N`? (3 marks)

**C2.** (8 marks) A plane passes through `P(1, 1, 0)`, `Q(1, 0, 1)`, and `R(0, 1, 1)`. Seen from outside, `P → Q → R` is counter-clockwise.

(a) Find the outward normal. (2 marks)

(b) Find the unit outward normal. (2 marks)

(c) Write `aX + bY + cZ + d = 0` so that a positive value means the outside half-space. (2 marks)

(d) Classify `(1, 1, 1)` and `(0, 0, 0)`. Using the unit normal, give the signed distance from the origin to the plane, which is `−d`. (2 marks)

**C3.** (12 marks) An object is scaled by `(1, 1, 2)` about the origin, then rotated 90° counter-clockwise about the X axis, then translated by `(0, 0, 4)`.

(a) Write `S`, `RX(90°)`, and `T`. Explain why the composite that acts on a point is `T RX S`. (3 marks)

(b) Multiply the composite into one 4×4 matrix. (3 marks)

(c) Find the images of `(0, 1, 0)` and of the origin. (2 marks)

(d) Write the three OpenGL calls, in an order consistent with (a). (2 marks)

(e) A different rotation is 90° counter-clockwise about the line that passes through `F = (0, 2, 0)` and is parallel to X. Write the composite as a product of three elementary matrices, without multiplying it out, and write the matching OpenGL calls. (2 marks)

**C4.** (12 marks) Viewing and projection.

(a) The camera is at `(0, 4, 4)`, looking at the world origin, with `VUP = (0, 1, 0)`. Using the lecture definition of VPN, find the unit vectors `Xvc`, `Yvc`, and `Zvc`, and the matrix `M_{VC ← WC}`. The given VUP is not perpendicular to VPN. Do not use it as `Yvc`. (5 marks)

(b) All quantities below are already in VC. The view plane is `Z = 0` and `Vp = (1, 1, 1)`. Compute the foreshortening ratio, name the projection as orthographic, Cavalier, Cabinet, or general oblique, and write the 4×4 parallel matrix. If you keep OpenGL’s depth row, say so. (3 marks)

(c) An orthographic projection uses the view plane `Z = −50`. The window is centred at `(100, 150)`, with width 80 and height 60. The far plane is `Z = −400`. Write the geometric 4×4 matrix, whose third row places Z on the view plane, and write the `glOrtho` call. (2 marks)

(d) The PRP is at the VC origin and the view plane is `Z = −4`. Write the lecture perspective matrix, apply it to `(8, 0, −8, 1)`, divide by W, and state `(xp, yp)`. (2 marks)

---

## Section D. Code

20 marks. Write C and fixed-function OpenGL.

**D1.** (8 marks) The mesh is a super-ellipsoid centred at `(0, 0, 10)`, with radii `rx = 2`, `ry = 3`, and `rz = 4`. The exponents `s1` and `s2` are arguments. `N` and `M` are greater than 1. Assume `sgn` is the lecture function: it returns `1`, `−1`, or `0`. Complete every blank. State the ranges of `φ` and `θ`. In one sentence, say why `pow(cp, s1)` is not safe, and name the surface obtained when `s1 = s2 = 1`.

```c
for (int i = 0; i < N; i++) {
    double phi = ____________________;
    for (int j = 0; j < M; j++) {
        double theta = ____________________;
        double cp = cos(phi), sp = sin(phi);
        double ct = cos(theta), st = sin(theta);
        mesh[i][j].x = ____________________;
        mesh[i][j].y = ____________________;
        mesh[i][j].z = ____________________;
    }
}
```

**D2.** (8 marks)

(a) Write a fragment that draws a closed cylinder of radius 20 and height 50. The base lies on the XZ plane and the axis runs along +Y. Use 32 slices and 1 stack. Include the rotation, both caps, and a matching push/pop pair. In one comment, show where `(0, 0, 1)` goes under that rotation. (6 marks)

(b) A generalized cylinder uses the course mesh for a profile that lies in `z = 0` and is rotated about Y: `x = X cos β`, `y = Y`, `z = X sin β`. One profile point is `(X, Y) = (−0.6, 0.5)`. Evaluate the mesh point at `β = 0` and at `β = π/2`. (2 marks)

**D3.** (4 marks) Read the program. Write the current composite matrix `C`, and find the image of `(1, 0, 0)`.

```c
glMatrixMode(GL_MODELVIEW);
glLoadIdentity();
glTranslatef(0, 0, 5);
glRotatef(90, 1, 0, 0);
glTranslatef(0, 2, 0);
```

---

End of the paper. No solutions are printed here.
