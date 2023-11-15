# DMF_Trace_Formula

This repository contains MAGMA code to compute traces, characteristic polynomials, and slopes of Hecke operators on Drinfeld modular forms via the trace formula.

The algorithms are contained in the file DMF_Trace_Formula. There are also some files containing sample data which have been computed using the algorithms.

Let T_P be a Hecke operator. An advantage of the trace formula is that the set of data needed to compute the trace of (T_P)^n on S_{k,l} does not depend on k and l. (This data consists of Weil numbers of isomorphism classes of Drinfeld modules with characteristic P over GF(q^{n*deg(P)}).) Therefore, many of the algorithms become quite efficient once this data has been computed once and stored as a list. The algorithms are mostly designed with this in mind, but there are also functions which don't require the input of a stored list.

Sample code to compute the trace of T_P on S_{k,l} for q = 3, P = T, 1 < k < 101, and any type:

load "DMF_Trace_Formula";
L := IsogClassList(3,1,Polynomial([0,1]));
for l := 0 to 1 do
  for k := 2 to 100 do
    printf "(%o,%o): ",k,l;
    TraceFromList(k,l,3,L);
  end for;
end for;

To compute the T-adic slopes of T_P on S_{k,l} for q = 3, P = T, k = 40, l = 0, one simply types

THeckeSlopes(40,0,3,Polynomial([0,1]));

To compute the T-adic slopes of T_P on S_{k,l} for various k and l, it is more efficient to first create lists of isomorphism classes of Drinfeld modules; then use these to compute lists of traces of powers of T_P on S_{k,l} for various k and l; then use the function CharPolFromList to compute the characteristic polynomials; and finally use the function Slopes(f,Zeros(T)[1]) as f ranges over these characteristic polynomials.
