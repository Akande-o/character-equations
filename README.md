# character-equations
Introduction
Character equation is a type of logic puzzle that can look like this:

A + AB + ACC == BCCC
Each such expression represents a mathematical equation in which some numerals are replaced by characters. (These characters often form words which make the puzzle more entertaining and attractive.) Your task is to replace the characters by digits such that the equation holds. For example, in the above equation we can replace all occurences of A with digit 9, B with 1, and C with 0, and we get

9 + 91 + 900 == 1000
which is a correct mathematical equation. It is also a Python expression which evaluates to True.

Another example of character equation may be the following puzzle and its solution:

(J + O + I + N + T)**3 == JOINT
(1 + 9 + 6 + 8 + 3)**3 == 19683
Further requirements for valid solutions:

The solution is a mutually unique assignment of digits and letters. The same letters always represent the same digits, different letters must represent different digits. E.g. if you decide that letter P represents digit 6, you have to substitute this digit for all the Ps in the equation, and also no other letter can represent digit 6.
The first letters of all “words” (including single-character “words”) cannot represent digit 0, since we usually do not write the initial zeros. (In the first example above, neither A, nor B can be 0. In the second example, no character can be zero, since all are part of single-character words.)
Published character equations usually have only a single solution. In general (and in this task in particular), this feature is not always fulfilled. We would like to find all possible solutions.

Specifications
In module char_equations.py create function solve() which shall be able to solve character equations. The input shall be a single string with the character equation, and the function shall return a list of strings which represent all the valid numeric solutions.

def solve(equation):
    """Find all solutions to the given character equation
 
    :param equation: string, the specification of the character equation
    :return: list of strings, solutions to the equation, 
                 all characters are replaced by numbers and the equation holds; 
             empty list, if no solution is found.
 
    >>> solve('A + AB + ACC == BCCC')
    ['9 + 91 + 900 == 1000']
    >>> solve('(J + O + I + N + T)**3 == JOINT')
    ['(1 + 9 + 6 + 8 + 3)**3 == 19683']
    >>> solve('ABC + ADC == DECA')  # Two solutions!!!
    ['834 + 814 == 1648', '879 + 819 == 1698']
    """
Function solve() shall be able to handle various types of equations, not only those that contain several summands on the left-hand side, and result on the right-hand side, see e.g. the equation (J + O + I + N + T)**3 == JOINT, which contains the third power (and other types of operations are possible too).

We also expect your code to run at most several minutes to find solutions of the most complex equations (i.e. those containing the maximum of 10 different letters).

Suggestions for elaboration
We expect you will implement a brute-force solution, i.e. you will test all possible assignments of digits to characters. The follwing things may come handy:

How to find all unique letters in a string? You should be able to do this.
How to find the initial letters of “words”? You should be able to do this too.
How to generate a permutation of numbers for assignment to letters?
itertools.permutations()
Usage example: How to generate all possible pairs made of digits 0, 1, 2 a 3? The following code
import itertools
for perm in itertools.permutations('0123', 2):
    print(''.join(perm), end=' ')
shall produce the following output:
01 02 03 10 12 13 20 21 23 30 31 32 
How to easilly substitute some letters in a string with others?
str.translate(), str.maketrans()
Usage example: How to replace some of the uppercase letters with lowercase? The following code
chars_to_replace = 'AEIOU'
replace_with_chars = 'aeiou'
# Create the translation table (map)
tab = str.maketrans(chars_to_replace, replace_with_chars)
in_string = 'THIS SENTENCE IS TO BE CHANGED'
# Transform the input string to a new one using the translation table
out_string = in_string.translate(tab)
print(out_string)
shall produce the following output:
THiS SeNTeNCe iS To Be CHaNGeD
How to evaluate a Python expression stored in a string?
eval()
Usage example:
>>> eval('1 + 1')
2
>>> eval('1 + 1 == 2')
True
You can further test your solution on the following character equations (only the number of solutions is provided):

GO + MOO + GO == LAME                (1 solution)
ABC + CBA == DDD                     (12 solutions)
VIOLIN * 2 + VIOLA == TRIO + SONATA  (4 solutions)
NORTH / SOUTH == EAST / WEST         (1 solution)
