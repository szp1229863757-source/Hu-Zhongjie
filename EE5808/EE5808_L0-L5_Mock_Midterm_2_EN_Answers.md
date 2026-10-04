# EE5808 Mock Midterm 2 — Answer Key

Finish the paper before you open this key. Equivalent forms are accepted when the steps and the signs are right.

### Marking

A reversed sign loses most of that part. Later algebra that follows the student’s own sign correctly can still earn method marks. An OpenGL order that disagrees with the matrix does not get full marks for that part. Writing VPN as look-at point − eye reverses the camera frame and receives at most the method marks for that part. Swapping the Cavalier ratio with the Cabinet ratio loses both names.

---

## Section A (20 marks)

| Item | Verdict | One-line reason |
|---|---|---|
| A1 | **F** | The cross product uses sine: `\|A × B\| = \|A\| \|B\| sin α`. The dot product uses cosine. |
| A2 | **F** | `R^{−1} = Rᵀ` holds for a pure rotation. A matrix that also contains a translation is not orthogonal, so its inverse is not its transpose. |
| A3 | **F** | From the outside, a front face is counter-clockwise. A hidden back face looks clockwise. |
| A4 | **F** | The lecture order is `Xvc = \|VUP × VPN\|`. The swapped cross product reverses X and produces a left-handed frame. |
| A5 | **T** | `gluCylinder` runs along +Z from `z = 0` to `z = height`. An axis along +Y needs an extra rotation. |
| A6 | **T** | `glRotatef` rotates about a line through the current origin. An axis through another point still needs a translation to the origin and back. |
| A7 | **F** | The linear part has determinant `−1`, so counter-clockwise vertices become clockwise and the outward normal flips. The mirrored shape can still be correct. |
| A8 | **F** | `−Vp` is the same line. The foreshortening ratio, `xp`, and `yp` are unchanged. |
| A9 | **T** | Isometric projection is orthographic, not oblique and not perspective. The direction is parallel to a space diagonal `(±1, ±1, ±1)`. |
| A10 | **F** | The fourth row is `(0, 0, 1/zvp, 0)`. The Euclidean coordinates appear only after dividing by W. |

---

## Section B (20 marks)

### B1 (5 marks)

(a) Divide by `W = −3`:

`(6, −3, 9, −3) → (−2, 1, −3)`.

An ordinary point needs `W ≠ 0`. `W = 0` does not represent a Euclidean point. The usual choice for a finite point is `W = 1`. (2 marks)

(b) The origin of C2 is `(4, 0, 0)` measured in C1, and the axes are parallel, so a C1 coordinate is converted by subtracting that origin:

`M_{C2 ← C1} = T(−4, 0, 0)`

`M_{C2 ← WC} = T(−4, 0, 0) M_{C1 ← WC}`

Check: the point `(4, 0, 0)` in C1 must become the origin of C2. The opposite translation `T(+4, 0, 0)` sends it to `(8, 0, 0)`. (3 marks)

### B2 (5 marks)

(a) Only three of `a, b, c, d` are free. Multiplying all four by the same nonzero constant does not change the plane. If `(a, b, c)` is a unit normal, `−d` is the signed distance from the origin to the plane. The positive side is the side the normal points to. (2 marks)

(b) A face may be a list of vertices or a list of edges. Either is acceptable if the answer says which one it is. Attribute-table examples include `ka`, `kd`, `ks`, the specular exponent `ns`, and transparency `α`. Any two of these earn the mark. The full lighting formula is not required. (1 mark)

(c) A point is inside a convex solid exactly when `aX + bY + cZ + d < 0` for every face, with `(a, b, c)` the outward normal. Omitting one face makes the test incomplete. A concave solid is split into convex pieces, and the point is inside if it lies in any piece. If the split is impractical, cast a ray and use the odd/even count. A grazing hit is degenerate; cast several rays in random directions and take a majority vote. One use of the ray test is collision detection during a VR walk. (2 marks)

### B3 (5 marks)

(a) The same matrix can be a physical motion of an object inside one coordinate system, or a change of frame for one fixed point. (2 marks, together with the symbol)

`P(j) = M_{j ← i} P(i)`

(b) The frame, treated as an object, was enlarged by 2. A length measured in the enlarged frame is half of the length measured in frame 2, so the coordinate change is the inverse scale:

`M_{3 ← 2} = S(2, 2, 2)^{−1} = S(1/2, 1/2, 1/2)`

The inverse reverses a product:

`(T S)^{−1} = S^{−1} T^{−1}`

(1 mark)

(c) The camera frame rotates by `+60°` about its own Z, so a fixed world point appears rotated by `−60°` in the new camera. The new factor stands on the left:

`M_new = RZ(−60°) M_old`

This is Lecture 3’s rule 1: if the frame, treated as an object, rotates by `+θ`, point coordinates change by `−θ`. (2 marks)

### B4 (5 marks)

(a) `glPopMatrix` restores the matrix saved by the matching `glPushMatrix`. It does not restore the identity. Inside a part, the pair keeps a local translation or scale from leaking to the caller. At a branch, the pair returns to the parent so the next child does not inherit its sibling. (2 marks)

(b) Each call is relative to the result of the previous call. (2 marks)

```c
glTranslatef( w/2,  l/2, 0);   /* right front  ( w/2,  l/2) */
glTranslatef(-w,     0,   0);   /* left front   (−w/2,  l/2) */
glTranslatef( 0,    -l,   0);   /* left rear    (−w/2, −l/2) */
glTranslatef( w,     0,   0);   /* right rear   ( w/2, −l/2) */
```

The right-rear wheel is at `(w/2, −l/2)`. A part inserted between two of these calls would carry every later wheel with it. A push/pop pair around each wheel avoids that.

Four absolute placements, each inside its own push/pop pair and ending at the same four positions, also receive full marks. The question asks for the accumulated form.

(c) (1 mark)

```text
| 1  0   2  0 |
| 0  1  −1  0 |
| 0  0   1  0 |
| 0  0   0  1 |
```

Column-major order reads down the columns:

```c
{1, 0, 0, 0,   0, 1, 0, 0,   2, -1, 1, 0,   0, 0, 0, 1}
```

Every affine transform maps parallel lines to parallel lines. This one mark needs the matrix, the column-major array, and that sentence. A row-major array does not receive the array portion.

---

## Section C (40 marks)

### C1 (8 marks)

(a) `A · B = 1·2 + 2·(−1) + 2·2 = 2 − 2 + 4 = 4`.

`|A| = √(1 + 4 + 4) = 3`, `|B| = √(4 + 1 + 4) = 3`.

`cos α = 4 / (3·3) = 4/9`.

The angle is acute because the cosine is positive. (2 marks)

(b)

```text
A × B = (2·2 − 2·(−1),  2·2 − 1·2,  1·(−1) − 2·2)
      = (4 + 2,  4 − 2,  −1 − 4)
      = (6, 2, −5)
```

`A · (A × B) = 6 + 4 − 10 = 0`.

`B · (A × B) = 12 − 2 − 10 = 0`.

Both dot products vanish, so the cross product is perpendicular to A and to B. (3 marks)

(c) `N = (1/3, 2/3, 2/3)` and `L = (2/3, −1/3, 2/3)`.

`N · L = (2 − 2 + 4) / 9 = 4/9`.

`I_diff = (1/4) · 8 · (4/9) = 8/9`.

For `−N`, the dot product is `−4/9 < 0`. The light is behind the surface, so `I_diff = 0`. (3 marks)

### C2 (8 marks)

`Q − P = (0, −1, 1)` and `R − P = (−1, 0, 1)`.

(a)

```text
n = (Q − P) × (R − P)
  = ((−1)·1 − 1·0,  1·(−1) − 0·1,  0·0 − (−1)·(−1))
  = (−1, −1, −1)
```

The problem states that `P → Q → R` is counter-clockwise from the outside, so this cross product is the outward normal. Do not flip the sign. (2 marks)

(b) `|n| = √3`, so

`n̂ = (−1/√3, −1/√3, −1/√3)`. (2 marks)

(c) `n · ((X, Y, Z) − P) = 0`:

```text
−(X − 1) − (Y − 1) − Z = 0
−X − Y − Z + 2 = 0
```

A positive value is the outside half-space. Multiplying through by `−1` would flip the normal and is not the required equation. (2 marks)

(d) At `(1, 1, 1)`: `−1 − 1 − 1 + 2 = −1 < 0`, inside half-space.

At `(0, 0, 0)`: `+2 > 0`, outside half-space.

Divide the equation by `√3` to make the normal a unit vector:

`−X/√3 − Y/√3 − Z/√3 + 2/√3 = 0`,

so `d = 2/√3` and the signed distance from the origin to the plane is `−d = −2/√3`.

The ordinary distance is `2/√3`. The negative sign means that, starting at the origin, the plane is reached by moving against the outward normal. The origin itself is on the positive side, which agrees with the value `+2` of the un-normalized equation. (2 marks)

### C3 (12 marks)

(a) The point is scaled first, then rotated, then translated, so the composite is `M = T RX S`. (3 marks)

```text
S = | 1  0  0  0 |     RX(90°) = | 1  0  0  0 |     T = | 1  0  0  0 |
    | 0  1  0  0 |                | 0  0 −1  0 |         | 0  1  0  0 |
    | 0  0  2  0 |                | 0  1  0  0 |         | 0  0  1  4 |
    | 0  0  0  1 |                | 0  0  0  1 |         | 0  0  0  1 |
```

`RX(90°)` comes from `cos 90° = 0` and `sin 90° = 1` in the lecture matrix. The `(2, 3)` entry is `−sin 90° = −1`, and the `(3, 2)` entry is `sin 90° = 1`.

(b) `RX S` scales the third column of `RX` by 2:

```text
RX S = | 1  0   0  0 |
       | 0  0  −2  0 |
       | 0  1   0  0 |
       | 0  0   0  1 |
```

Left-multiplication by `T(0, 0, 4)` adds 4 to the `(3, 4)` entry:

```text
M = | 1  0   0  0 |
    | 0  0  −2  0 |
    | 0  1   0  4 |
    | 0  0   0  1 |
```

(3 marks)

(c) `(0, 1, 0, 1) → (0, 0, 5, 1)`. The origin `(0, 0, 0, 1) → (0, 0, 4, 1)`. (2 marks)

Check without the matrix. Scaling leaves `(0, 1, 0)` unchanged. A positive 90° turn about X sends the Y axis toward Z, so `(0, 1, 0)` becomes `(0, 0, 1)`. The translation then adds `(0, 0, 4)` and produces `(0, 0, 5)`. The origin is fixed by the scale and by the rotation about the origin, then moves to `(0, 0, 4)`.

(d) The call written last is applied first, so the scale is the last source line. (2 marks)

```c
glTranslatef(0, 0, 4);
glRotatef(90, 1, 0, 0);
glScalef(1, 1, 2);
```

(e) Translate `F` to the origin, rotate, then translate back. (2 marks)

`M = T(0, 2, 0) RX(90°) T(0, −2, 0)`

```c
glTranslatef(0, 2, 0);
glRotatef(90, 1, 0, 0);
glTranslatef(0, -2, 0);
```

A single `glRotatef` would rotate about the current origin, not about `(0, 2, 0)`.

### C4 (12 marks)

(a) `center = (0, 0, 0)` and `eye = (0, 4, 4)`, so

`VPN = eye − center = (0, 4, 4)`, `|VPN| = √(16 + 16) = √32 = 4√2`.

`Zvc = |VPN| = (0, 1/√2, 1/√2) = (0, √2/2, √2/2)`.

`VUP × Zvc = (0, 1, 0) × (0, 1/√2, 1/√2) = (1/√2, 0, 0)`.

Its length is `1/√2`, so the unit axis is `Xvc = (1, 0, 0)`.

The same X is obtained from the un-normalized cross product `(0, 1, 0) × (0, 4, 4) = (4, 0, 0)`.

`Yvc = Zvc × Xvc = (0, 1/√2, −1/√2) = (0, √2/2, −√2/2)`.

`Yvc` is not the given VUP. Their dot product is `1/√2 > 0`, so VUP still lies in the upper half of the `Zvc`–`Yvc` plane. The component of VUP parallel to VPN has been removed.

```text
Xvc · VRP = 0
Yvc · VRP = (1/√2)·4 + (−1/√2)·4 = 0
Zvc · VRP = (1/√2)·4 + (1/√2)·4 = 8/√2 = 4√2
```

```text
M_{VC ← WC} =
| 1    0       0      0   |
| 0   1/√2   −1/√2    0   |
| 0   1/√2    1/√2  −4√2  |
| 0    0       0      1   |
```

Check: the eye `(0, 4, 4)` maps to the origin. The third row gives `4/√2 + 4/√2 − 4√2 = 4√2 − 4√2 = 0`.

Writing VPN as `center − eye` reverses all three axes. That answer receives at most 2 method marks. (5 marks: VPN 1, three unit axes 3, translation column 1.)

(b) The foreshortening ratio is

`√(1² + 1²) / |1| = √2`.

`tan α = 1/√2`, so `α = arctan(1/√2)`.

The ratio is neither `0`, nor `1`, nor `1/2`. This is a general oblique projection. It is not orthographic, Cavalier, or Cabinet.

With `zvp = 0`, `Vpx/Vpz = 1` and `Vpy/Vpz = 1`:

`xp = X − Z`, `yp = Y − Z`.

```text
| 1  0  −1  0 |
| 0  1  −1  0 |
| 0  0   0  0 |     geometric third row, Z becomes 0
| 0  0   0  1 |
```

The OpenGL depth convention replaces the third row by `(0, 0, 1, 0)` and keeps the original Z. That form receives full marks when the answer says so. (3 marks)

(c) Half of the width is 40 and half of the height is 30, so the window is `X ∈ [60, 140]` and `Y ∈ [120, 180]`. The near plane `Z = −50` means the positive distance `dnear = 50`. The far plane `Z = −400` means `dfar = 400`.

```text
| 1  0  0    0 |
| 0  1  0    0 |
| 0  0  0  −50 |
| 0  0  0    1 |
```

```c
glOrtho(60, 140, 120, 180, 50, 400);
```

The near and far arguments are positive distances. Writing `glOrtho(..., -50, -400)` is wrong. (2 marks)

(d) `zvp = −4`, so the fourth row is `(0, 0, 1/(−4), 0) = (0, 0, −1/4, 0)`:

```text
| 1  0   0     0 |
| 0  1   0     0 |
| 0  0   1     0 |
| 0  0  −1/4   0 |
```

`(8, 0, −8, 1) → (8, 0, −8, 2)`, because `W' = Z / zvp = (−8)/(−4) = 2`.

Divide by W: `(4, 0, −4, 1)`. Therefore `(xp, yp) = (4, 0)`.

The similar-triangle check is `xp = 8 · (−4) / (−8) = 4` and `yp = 0`. The projected point lies on the view plane `Z = −4`. (2 marks)

---

## Section D (20 marks)

### D1 (8 marks)

`φ ∈ [−π/2, π/2]` and `θ` covers one full turn. The lecture longitude starts at `−π`; starting at `0` is accepted when the samples still close the circle. The two angle lines, including those ranges, are worth 2 marks.

```c
for (int i = 0; i < N; i++) {
    double phi = -PI/2.0 + i * PI / (N - 1);
    for (int j = 0; j < M; j++) {
        double theta = -PI + j * 2.0 * PI / (M - 1);
        double cp = cos(phi), sp = sin(phi);
        double ct = cos(theta), st = sin(theta);
        mesh[i][j].x = 2 * sgn(cp)*pow(fabs(cp), s1) * sgn(ct)*pow(fabs(ct), s2);
        mesh[i][j].y = 3 * sgn(cp)*pow(fabs(cp), s1) * sgn(st)*pow(fabs(st), s2);
        mesh[i][j].z = 10 + 4 * sgn(sp)*pow(fabs(sp), s1);
    }
}
```

The `x` and `y` lines are worth 2 marks together, and the `z` line is worth 2 marks. The centre offset `10` belongs on Z only, and Z does not depend on `θ`.

`pow(cp, s1)` is not safe because a non-integer power of a negative number is not the real value required here. The lecture form is `sgn(t) · |t|^s`. (1 mark)

When `s1 = s2 = 1` the surface is an ellipsoid. It is not a sphere, because the three radii differ. Equal radii together with `s1 = s2 = 1` would give a sphere. For those two exponents the `sgn` and `fabs` factors agree with ordinary products of `cos` and `sin`, but they should stay in the general code. (1 mark)

### D2 (8 marks)

(a) `gluCylinder` is born along +Z. A rotation of `−90°` about X sends `(0, 0, 1)` to `(0, 1, 0)`, so the axis lies along +Y and the base lies on the XZ plane. The side and the two disks are three meshes, not one quadrilateral mesh. (6 marks)

```c
GLUquadric *q = gluNewQuadric();
glPushMatrix();
glRotatef(-90, 1, 0, 0);              /* (0,0,1) -> (0,1,0); +Z becomes +Y */
gluCylinder(q, 20, 20, 50, 32, 1);    /* radius 20, height 50 */
gluDisk(q, 0, 20, 32, 1);             /* base on the XZ plane */
glTranslatef(0, 0, 50);               /* along the cylinder axis, local Z */
gluDisk(q, 0, 20, 32, 1);             /* cap at height 50 */
glPopMatrix();
```

Any fragment that puts the base on XZ, the axis along +Y, and the cap at height 50 receives the marks. Missing either cap, or leaving the axis along +Z, loses the corresponding part. The push/pop pair is worth 1 of the 6 marks.

(b) Keep the signed profile coordinate. It is a signed radius, not `|X|`.

`β = 0`: `(−0.6, 0.5, 0)`.

`β = π/2`: `(0, 0.5, −0.6)`, because `z = X sin(π/2) = −0.6`.

The standard matrix `RY(+β)` would instead give `z = −X sin β = +0.6` at `β = π/2`. This item follows the course mesh stated in the question, `z = X sin β`. (2 marks)

### D3 (4 marks)

Post-multiplication means the last call is applied to the vertex first:

`C = T(0, 0, 5) RX(90°) T(0, 2, 0)`.

```text
RX(90°) T(0, 2, 0) = | 1  0   0  0 |
                     | 0  0  −1  0 |
                     | 0  1   0  2 |
                     | 0  0   0  1 |

C = | 1  0   0  0 |
    | 0  0  −1  0 |
    | 0  1   0  7 |
    | 0  0   0  1 |
```

`(1, 0, 0, 1) → (1, 0, 7, 1)`.

Check along the calls. `T(0, 2, 0)` sends `(1, 0, 0)` to `(1, 2, 0)`. `RX(90°)` sends `(x, y, z)` to `(x, −z, y)`, so `(1, 2, 0)` becomes `(1, 0, 2)`. `T(0, 0, 5)` then produces `(1, 0, 7)`.

The matrix is worth 3 marks and the image is worth 1 mark. Writing the factors in source-line order, `T(0, 2, 0) RX T(0, 0, 5)`, contradicts post-multiplication and does not receive the marks for this item.

---

## Mark total

| Question | Marks |
|---|---|
| A1–A10 | 20 |
| B1–B4 | 20 |
| C1 | 8 |
| C2 | 8 |
| C3 | 12 |
| C4 | 12 |
| D1 | 8 |
| D2 | 8 |
| D3 | 4 |
| **Total** | **100** |
