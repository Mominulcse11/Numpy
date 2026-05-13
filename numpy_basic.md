# NumPy: The Absolute Basics — Main Points

---

## 1. What is NumPy?
- **NumPy (Numerical Python)** is an open-source Python library for science and engineering.
- Core structure: **`ndarray`** — an N-dimensional, homogeneous array.
- Shines when working with large quantities of **same-type (homogeneous)** data on the CPU.
- Import convention: `import numpy as np`

---

## 2. What is an Array?
- A structure for storing and retrieving data, visualized as a grid.
- **1D** → list, **2D** → table, **3D** → stacked tables, **N-D** → generalized.
- NumPy array restrictions:
  - All elements must be the **same data type**.
  - Total **size is fixed** after creation.
  - Shape must be **rectangular** (no jagged arrays).

---

## 3. Array Fundamentals
- Created from Python sequences (lists).
- **0-indexed** — first element is at index `0`.
- Arrays are **mutable**.
- Slicing an array returns a **view** (not a copy) — changes to the view affect the original.
- Multi-dimensional arrays use comma-separated indices: `a[row, col]`.

---

## 4. Array Attributes
| Attribute | Description |
|-----------|-------------|
| `ndim`    | Number of dimensions (axes) |
| `shape`   | Tuple of element counts per dimension |
| `size`    | Total number of elements (`product of shape`) |
| `dtype`   | Data type of elements (e.g. `int64`, `float64`) |

---

## 5. Creating Arrays
| Function | Description |
|----------|-------------|
| `np.zeros(n)` | Array of zeros |
| `np.ones(n)` | Array of ones |
| `np.empty(n)` | Uninitialized array (fast) |
| `np.arange(start, stop, step)` | Range of values |
| `np.linspace(start, stop, num)` | Evenly spaced values |
| `dtype=` keyword | Specify data type explicitly |

---

## 6. Adding, Removing & Sorting
- `np.sort(arr)` → sorted copy (ascending by default).
- Other sort tools: `argsort`, `lexsort`, `searchsorted`, `partition`.
- `np.concatenate((a, b))` → joins arrays along an axis.
- Remove elements by **indexing** only the elements you want to keep.

---

## 7. Shape & Size of an Array
- `ndarray.ndim` → number of axes.
- `ndarray.size` → total elements.
- `ndarray.shape` → tuple of dimension sizes.

---

## 8. Reshaping
- `arr.reshape(new_shape)` → new shape, same data, same total size required.
- `order` parameter: `'C'` (row-major), `'F'` (column-major), `'A'` (auto).

---

## 9. Adding a New Axis (1D → 2D)
- `np.newaxis` increases dimensions by 1 when used in indexing.
- `np.expand_dims(a, axis=n)` inserts an axis at position `n`.
- Row vector: `a[np.newaxis, :]` → shape `(1, n)`
- Column vector: `a[:, np.newaxis]` → shape `(n, 1)`

---

## 10. Indexing & Slicing
- Same syntax as Python lists: `data[0]`, `data[0:2]`, `data[-2:]`.
- **Boolean indexing**: `a[a < 5]`, `a[a >= 5]`, `a[a % 2 == 0]`.
- **Multiple conditions**: `a[(a > 2) & (a < 11)]`, `(a > 5) | (a == 5)`.
- `np.nonzero(condition)` → returns indices of elements that satisfy the condition.
- The universal formula is array[start:stop:step]


---

## 11. Creating Arrays from Existing Data
| Function | Description |
|----------|-------------|
| `a[3:8]` | Slice a section |
| `np.vstack((a1, a2))` | Stack vertically |
| `np.hstack((a1, a2))` | Stack horizontally |
| `np.hsplit(arr, n)` | Split into n equal arrays |
| `.view()` | Shallow copy (shares data) |
| `.copy()` | Deep copy (independent) |

---

## 12. Basic Array Operations
- Element-wise: `+`, `-`, `*`, `/` between arrays of the same shape.
- Aggregation: `.sum()`, `.min()`, `.max()`, `.mean()`, `.prod()`, `.std()`.
- Use `axis=0` to aggregate **across rows** (per column); `axis=1` **across columns** (per row).

---

## 13. Broadcasting
- Allows operations between arrays of **different shapes**.
- NumPy stretches a scalar (or smaller array) to match the shape of the larger one.
- Dimensions must be **equal or one of them must be 1**.
- Incompatible shapes raise a `ValueError`.

---

## 14. Creating Matrices
- 2D arrays are created from nested lists.
- Matrix indexing: `data[row, col]`, `data[1:3]`, `data[0:2, 0]`.
- Aggregate across axes with `axis=0` (columns) or `axis=1` (rows).
- Matrix arithmetic works element-wise when shapes match.
- Broadcasting applies when one matrix has a single row or column.

---

## 15. Generating Random Numbers
- `np.random.default_rng()` → modern recommended way to create a generator.
- `rng.random(n)` → floats in [0, 1).
- `rng.integers(high, size=(r, c))` → random integers (low inclusive, high exclusive).
- Essential for: weight initialization, data shuffling, train/test splits.

---

## 16. Unique Items & Counts
- `np.unique(a)` → sorted unique values.
- `return_index=True` → indices of first occurrences.
- `return_counts=True` → frequency of each unique value.
- `axis=0` → unique rows; `axis=1` → unique columns (for 2D arrays).

---

## 17. Transposing & Reshaping
- `arr.T` or `arr.transpose()` → transposes the matrix (swaps axes).
- `arr.reshape(r, c)` → changes shape without changing data.

---

## 18. Reversing an Array
- `np.flip(arr)` → reverses entire array.
- `np.flip(arr, axis=0)` → reverses rows only.
- `np.flip(arr, axis=1)` → reverses columns only.
- Can also reverse a single row or column by targeting it directly.

---

## 19. Flattening Multidimensional Arrays
| Method | Returns | Modifying affects original? |
|--------|---------|----------------------------|
| `.flatten()` | Copy | No |
| `.ravel()` | View (usually) | Yes |

---

## 20. Accessing Documentation
- `help(obj)` → Python built-in help.
- `obj?` → IPython shorthand for docs.
- `obj??` → shows source code (IPython).
- Add docstrings to your own functions with `""" """`.

---

## 21. Mathematical Formulas
- NumPy makes implementing formulas (like **Mean Squared Error**) simple and readable.
- Operations apply element-wise across entire arrays automatically.
- Example MSE: `error = (1/n) * np.sum((predictions - labels) ** 2)`

---

## 22. Saving & Loading Arrays
| Function | Format | Use Case |
|----------|--------|----------|
| `np.save('file', arr)` | `.npy` | Single array (binary) |
| `np.savez('file', arr)` | `.npz` | Multiple arrays |
| `np.savetxt('file.csv', arr)` | `.csv`/`.txt` | Human-readable text |
| `np.load('file.npy')` | `.npy` | Load binary |
| `np.loadtxt('file.csv')` | `.csv` | Load text |

---

## 23. Importing/Exporting CSV with Pandas
- `pd.read_csv('file.csv').values` → read CSV into NumPy array.
- `pd.DataFrame(arr).to_csv('file.csv')` → export array to CSV.
- `np.savetxt('file.csv', arr, fmt='%.2f', delimiter=',', header='...')` → NumPy-native CSV save.

---

## 24. Plotting with Matplotlib
- `import matplotlib.pyplot as plt`
- `plt.plot(a)` → line plot from array.
- `plt.plot(x, y, 'purple')` → styled line; `plt.plot(x, y, 'o')` → dot plot.
- 3D surface plot using `fig.add_subplot(projection='3d')` and `ax.plot_surface(X, Y, Z)`.
- Use `%matplotlib inline` in Jupyter to display plots inline.