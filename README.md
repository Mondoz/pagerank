# An Open Source PageRank Implementation

This project provides an open source PageRank implementation. The
implementation is a straightforward application of the algorithm
description given in the American Mathematical Society's Feature
Column [How Google Finds Your Needle in the Web's
Haystack](http://www.ams.org/samplings/feature-column/fcarc-pagerank),
by David Austing. It can handle very big hyperlink graphs with
millions of vertices and arcs.

# Building

The project is written in standard C++ and can be built by running:

    g++ -o pagerank pagerank.cpp table.cpp table.h

# Usage

pagerank is invoked by

    pagerank [OPTIONS] graph_file

where OPTIONS may be:

* -t: if set, tracing is enabled. Tracing outputs all intermediate
   steps of the pagerank calculation algorithm and can be very
   voluminous.

* -n: if set, the graph_file is in numeric format, that is it consists
   of lines of the form `<from><delim><to>` where `<from>` and `<to>` are
   integer vertex indices, starting with zero. If not set, the
   graph_file consists of lines of the form `<from><delim><to>` where
   `<from>` and `<to>` and vertex IDs, and will be interpreted as strings.

* -a `<float>`: the pagerank dumping factor; default is  0.85.

* -c `<float>`: the convergence criterion. The pagerank iterations will
   stop when two successive iterations have converged to less than or
   equal to this value. Default is 0.00001.

* -s `<integer>`: the number of rows of the hyperlink matrix. This is
   not the maximum size; if the graph requires more rows, they will be
   allocated as necessary. If an approximate size is known beforehand,
   however, the necessary internal data structures can be
   pre-allocated for better performance.

* -d `<string>`: the delimited used to separate vector indices in the
   input graph file. Default is " => ".

# Testing

Testing the implementation was carried out by comparing with pagerank
calculations produced by [Jung](http://jung.sourceforge.net/). The
Java code that produced the calculations can be found in the java
directory of the project. The test suites can be found at the test
directory of the project, along with the test driver program
[pagerank_test.cpp](https://github.com/louridas/pagerank/blob/master/test/pagerank_test.cpp),
which is invoked by: `pagerank_test <test_suite>`.

The `<test_suite>` is a file containing in each line a filename, in the
same directory, with an input graph. For an input graph foo.txt, the
pagerank results against which we want to compare our implementation
is found in foo-pr.txt. The result files are generated by the
[pagerank_calc.sh script](https://github.com/louridas/pagerank/blob/master/test/pagerank_calc.sh).

The test driver is written in standard C++ and can be compiled with:

    g++ -I../cpp -o pagerank_test pagerank_test.cpp ../cpp/table.cpp 

The graph test files were generated by the
[igraph](http://igraph.sourceforge.net/) R port using the R scripts in
the test directory.
