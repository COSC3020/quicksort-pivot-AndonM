[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-718a45dd9cf7e7f842a935f5ebbe5719a5e09af4491e668f4dbf3b35d5cca122.svg)](https://classroom.github.com/online_ide?assignment_repo_id=11974282&assignment_repo_type=AssignmentRepo)
# Quicksort Pivots

in the lectures I only briefly mentioned strategies for determining a good pivot
for quicksort. The implementation on the slides simply picks the leftmost
element in the part of the array that we consider as a pivot. I also mentioned a
few other ways of picking a good pivot, e.g. randomly.

Median-of-three is also a good way of picking a pivot -- inspect the first,
middle, and last elements of the part of the array under consideration and
choose the median value. Using the probabilities for picking a pivot in a
particular part of the array (in the same way as we did on slide 34), argue
whether this method is more or less (or equally) likely to pick a good pivot
compared to simply choosing the first element. Assume that all permutations are
equally likely, i.e. the input array is ordered randomly.

Your answer must derive probabilities for choosing a good pivot and
quantitatively reason with them.

REFERENCED DHRUV8806'S QUICKSORT REPOSITORY

For the leftmost selection, the probability of obtaining a good pivot is 1/2. Further, we note that there is a 1/4 chance that we pick a pivot too small and a 1/4 chance of picking a pivot that is too large.

Moving to the median-of-three strategy with pivots (S, G, L) where S represents a pivot too small, G represents a good pivot, and L represents a pivot that is too large, we see the odds of S and L are both 1/4 and the odds of G are 1/2 akin to simply picking the leftmost value. Because we are picking the median value of these outcomes, we must of course consider all of the possible outcomes. We see this comes out to be the following:  

$GGG = (1/2)^3 = 1/8$  
$GGL = (1/2)^2 * (1/4) = 1/16$  
$SGG = (1/4) * (1/2)^2 = 1/16$  
$GLL = (1/2) * (1/4)^2 = 1/32$  
$SGL = (1/4) * (1/2) * (1/4) = 1/32$  
$SSG = (1/4)^2 * 1/2 = 1/32$   
$LLL = (1/4)^3 = 1/64$  
$SLL = (1/4) * (1/4)^2 = 1/64$  
$SSL = (1/4)^2 * (1/4) = 1/64$  
$SSS = (1/4)^3) = 1/64$  

Putting everything over a common denominator of 64 gives us the following probabilities:  

$GGG = 8/64$  
$GGL = 4/64$  
$SGG = 4/64$    
$GLL = 2/64$    
$SGL = 2/64$  
$SSG = 2/64$  
$LLL = 1/64$  
$SLL = 1/64$  
$SSL = 1/64$  
$SSS = 1/64$  

Now, we must consider all possible arrangements of pivot choices for these outcomes:

GGG has only one permutation, GGG, so our odds remain unchanged $(8/64)$  
GGL has three permutations, GGL, GLG, and LGG, so our odds become $3 * 4/64 = 12/64$  
SGG has three permutations, SGG, GSG, and GGS, so our odds become $3 * 4/64 = 12/64$  
GLL has three permutations, GLL, LGL, and LLG, so our odds become $3 * 2/64 = 6/64$  
SGL has six permutations, SGL, GSL, GLS, LGS, LSG, and SLG, so our odds become $6 * 2/64 = 12/64$   
SSG has three permutations, SSG, SGS, and GSS, so our odds become $3 * 2/64 = 6/64$  
LLL has one permutation, LLL, so our odds remain unchanged $(1/64)$  
SLL has three permutations, SLL, LSL, and LLS, so our odds become $3 * 1/64 = 3/64$  
SSL has three permutations, SSL, SLS, and LSS, so our odds become $3 * 1/64 = 3/64$  
SSS has one permutation so our odds remain unchanged $(1/64)$

With this in mind, we can now sum up all of the "good outcomes" resulting from the median-of-three strategy (the median value is a good pivot). We see that the outcomes in which this is the case are GGG, GGL, SGG, and SGL. Adding these together we see the median-of-three method will pick a good pivot $8/64 + 12/64 + 12/64 + 12/64 = 44/64$ which comes out to ~68%. From these results we conclude the median-of-three method will pick a better pivot compared to the leftmost value about (68 - 50) = 18% of the time.
