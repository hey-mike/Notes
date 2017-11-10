# Training Algorithms

## [Linear Algebra notes](http://www.cs.cmu.edu/~zkolter/course/linalg/linalg_notes.pdf)

## Numpy

- The advantage of using Numpy over classic Python for-loop structures is that its arithmetic operations are vectorized, imporve the performance of operations by making better use of **Single Instruction, Multiple Data (SIMD)** of moden CPU architecures.

methods

- **dot()**:dot product of two pioints
- **zip()**:The zip() function take iterables (can be zero or more), makes iterator that aggregates elements based on the iterables passed, and returns an iterator of tuples.
- **where**(condition[, x, y]): Return elements, either from x or y, depending on condition.i.e. np.where(y == 'Iris-setosa', -1, 1), where value equals 'Iris-setosa' will change to be -1.

## Pandas

methods

- **read_csv()**: read csv file , return *DataFrame*
- **tail()**: get last n line of DataFrame
- **iloc(array, index)**: get numer of rows of column index
