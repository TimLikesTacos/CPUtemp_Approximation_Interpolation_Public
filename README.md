
This is an application developed for a school project written in Rust. Since this project may be used for future use, the source code has been removed from this repository.  If you are not a student performing a similar project and want to see the source code, message me and I can provide.

 
# CPU Temperature Interpolation and Approximation

  

This is an application that reads temperature data for a 4-core CPU from a `.txt` file and performs these three calculations:

* 1) Global Least Squares Approximation.

* 2) Linear Interpolation

* 3) Cubic Spline Interpolation.

  

The Least Squares Approximation and Linear Interpolation equations are given in the form:

ϕ = c<sub>0</sub> + c<sub>1</sub> * x^1

The cubic spline interpolation is given in the form:

S(x) = S(x) = C<sub>0</sub> + C<sub>1</sub>*(x - x<sub>0</sub>) + C<sub>2</sub>*(x - x<sub>0</sub>)<sup>2</sup> + C<sub>3</sub>*(x<sub>0</sub>)<sup>3</sup>

  

Where X<sub>0</sub> is the value of X at the start of the subdomain. If it is desired to solve the cubic spline in terms of only X, as in the Least Squares and Linear Iterpolation, then the `simplify()` function in the interpolation module should be used. This is not done by default as it produces "ugly" results when printed out, as the magnitudes of the coefficents can become significantly large.

  

## Getting Started

  

Language used: Rust

# Requirements

  

* rustc 1.0 or greater

* cargo 1.0 or greater

  
  

## Crates that will be installed

  

The following additional crate is used:

  

```

regex = "0.2.11"

num = "0.2.1"

num-traits = "0.2.11"

string-builder = "0.2.0"

  

```

  

This crate is listed in the Cargo.toml file and will be downloaded when `cargo build` is run.

  
  

# Compilation

  

It is recommended to compile the code by using Cargo as follows:

```

cargo build --release

```

  
  

# Sample Execution & Output

  

The program can be run by:

  

```

./target/release/cpu_temp <filename>

```

  

or using cargo:

  

```

cargo run <filename>

```

  

The input file must be a text file containing four values in a row, separated by whitespace. They can have units adjacent to the numbers.

## Input file example

```

61.0 63.0 50.0 58.0

80.0 81.0 68.0 77.0

62.0 63.0 52.0 60.0

83.0 82.0 70.0 79.0

```

or

```

+61.0°C +63.0°C +50.0°C +58.0°C

+80.0°C +81.0°C +68.0°C +77.0°C

+62.0°C +63.0°C +52.0°C +60.0°C

+83.0°C +82.0°C +70.0°C +79.0°C

+68.0°C +69.0°C +58.0°C +65.0°C

```

will work.

  

If the input file was named `test_06_20_20.txt`, the command to run the application would be:

```

./target/release/cpu_temp test_06_20_20.txt

```

## Example output file name

The program will develop four different text files, each one coresponding to a different core. The file above will provide the following file names based off of the input file name:

```

test_06_20_20-core-0.txt

test_06_20_20-core-1.txt

test_06_20_20-core-2.txt

test_06_20_20-core-3.txt

```

  

## Sample output

Within each file, it will contain information on Least Squares Approximation, Linear Interpolation, and Cubic Spline Interpolation. For example,

file `test_06_20_20-core-0.txt` would contain:

```

0 <= x < 35610 ; y_0 = 77.15 + -0.00012x; least_squares

0 <= x < 30 ; y_0 = 61.00 + 0.63333x; interpolation

30 <= x < 60 ; y_1 = 98.00 + -0.60000x; interpolation

60 <= x < 90 ; y_2 = 20.00 + 0.70000x; interpolation

90 <= x < 120 ; y_3 = 128.00 + -0.50000x; interpolation

.

.

.

0 <= x < 30 ; y_0 = 61.00 + 1.08096(x-x0) + 0.00000(x-x0)^2 + -0.00050(x-x0)^3; cubic_spline

30 <= x < 60 ; y_1 = 80.00 + -0.26193(x-x0) + -0.04476(x-x0)^2 + 0.00112(x-x0)^3; cubic_spline

60 <= x < 90 ; y_2 = 62.00 + 0.06674(x-x0) + 0.06008(x-x0)^2 + -0.00130(x-x0)^3; cubic_spline

90 <= x < 120 ; y_3 = 83.00 + 0.16399(x-x0) + -0.05716(x-x0)^2 + 0.00117(x-x0)^3; cubic_spline

.

.

.

```

  
  

# Range of values

  

This program has been tested for values typically associated with CPU temperatures on the Celsius scale.

The program uses templated functions but non-integer number types such as floats or Rational should be used.

# Documentation

Documentation can be developed by running:

```

cargo doc --no-deps

```

and resulting Rust-docs can be found:

```

./target/doc/index.html

```
