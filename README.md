## Translate Python to C++

### Project Overview

The goal of this project is to take the python of the two dimensional histogram filter and translate it into C++.

Evaluate the correctness of code by compiling `tests.cpp` and then running the output. Do this by running the following from the command line.

    g++ tests.cpp
    ./a.out

### Project Tips

#### Project Files

There are only two files you need to worry about for this project: `helpers.cpp` and `localizer.cpp`. Here's what each file included in the starter code is for:

  - You can mostly ignore any `.h` (header) files, although if you add additional functions to .cpp files you should also define them within the related header file!
  - The `maps` folder just has data of the map data used in the project
  - `tests.cpp` is just for testing - no need to touch it
  - `debugging_helpers.cpp` is to help you debug; don't need to implement anything
  - `helpers.cpp` - Implement `normalize()` and `blur()`
  - `localizer.cpp` - Implement `initialize_beliefs()`, `sense()` and `move()`
  - `simulate.cpp` - You can uncomment portions of this to further help you develop the project, but this is not needed just to pass.
  
  
#### Initializing vectors & matrices in C++11

In older versions of C++, you could initialize the size of the vector or matrix to start, but you had to either replace each index or use `.push_back()` to place values within the vector. In C++11, this is made easier as you can place the values to begin with, as shown below (assuming the various `some_vals` shown below are already initialized or are a `const`):

    vector < vector <float> > our_matrix {{some_val1, some_val4, some_val7},
                                          {some_val2, some_val5, some_val8}, 
                                          {some_val3, some_val6, some_val9}};
                                          
Note that the values in the above should be floats given how the inner vector is defined; if they are doubles, you will likely get a compilation error due to loss of precision.


#### Modulo (%) in C++ and Negative Numbers

If you type `-1 % 5` into either Python script or Google, you should get `4` as the answer. However, if you do the same in C++, you'll get `1`.

Why? Well, it isn't actually modulo in C++, but the remainder!


#### Segmentation Faults
One potential cause of these is concerning modulo as described above, but there is also another potential cause.

Depending on your implementation, after you've coded `blur()`, running the out file from `tests.cpp` may produce a segmentation fault when the tests reach `move()` (i.e. `normalize()`, `blur()` and `initialize_beliefs()` will show their test results, and then the fault occurs). Typically this should resolve itself once `newGrid` within the `move()` function takes shape.


#### Additional Simulation (optional)
While all you need to pass the project is to pass all tests in `tests.cpp`, you can also visualize a simulation of your localizer with `simulate.cpp`. In order to do so, the first step is to uncomment all the lines at the bottom of the file around the `main()` function.

From here, it is up to you how to proceed - the map is initialized for you, and you can then call your functions from `localizer.cpp` to see what happens.

To see the results of the simulation, you'd run:

    g++ -std=c++11 simulate.cpp

Note that this is because you actually have a separate `main()` function here, so it is a completely separate program from `tests.cpp`.

There's one last item to note here - if you try to run `tests.cpp`, it actually uses the `Simulation` class from this file, and so trying to run `tests.cpp` while the `main()` function within `simulate.cpp` is uncommented will result in an error - make sure to comment it back out when submitting!
