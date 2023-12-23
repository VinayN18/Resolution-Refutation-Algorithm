Code was written in Python. I attached the ipynb file (Jupyter Source File).

The code was divided into three parts
--> Helper Functions - All the necessary functions used for the resolution-refutation algorithm which includes the Part-0 (Function which converts each formula into CNF) of the assignment

--> Implementing resolution-refutation algorithm posing it as an uninformed search problem

--> Implementing resolution-refutation algorithm posing it as an greedy search problem




# Helper Functions:
--> Operators: List containing propositional operators used for checking if any symbol matches with these list items or not

--> is_prop_operator(): Function is used to check whether operator is a propositional operator or not and returns it

--> segment_sentence(): Function parses the input sentence, identifies operators, skips the spaces and extracts literals and returns the list containing the operators and literals

--> forward_slice(): Function used to return the forward slice of sentence from index 

--> backward_slice(): Function used to return the backward slice of sentence

--> around_unary_op(): Function identifies occurrences of a specified unary operator (op) in the expression, encapsulates the operands of those operators with parentheses, and returns a modified list representing the processed expression. The function uses recursion to handle nested unary operations and iterates through the input sentence, updating it based on the identified unary operators. It returns the original expression with unary operators appropriately surrounded by parentheses

--> around_binary_op(): Function identifies occurrences of a specified binary operator (op) in the expression, encapsulates the operands of those operators with parentheses, and returns a modified list representing the processed expression. The function uses recursion to handle both left and right operands of the binary operation, iterates through the input sentence, and updates it based on the identified binary operators. It returns the original expression with binary operators appropriately surrounded by parentheses

--> induced_paranthesis(): Function applies a series of transformations using the functions around_unary_op() and around_binary_op(). Calls around_unary_op to encapsulate operands of the unary operator "!" with parentheses. Calls around_binary_op for each of the binary operators "&", "|", ">", and "=". Returns the modified sentence after applying the transformations. The operators are processed in the order of their precedence in standard logical operations (negation first, then conjunction, disjunction, implication, and equality)

--> literal_not_protected(): Function determines whether there is at least one literal (propositional symbol) in the logical expression that is not protected by parentheses. For each character in the sentence, if the character is not inside parentheses (i.e., when off_balance is zero), and it is not a parenthesis itself, the function returns True. This indicates that there is at least one unenclosed literal in the expression. If the loop completes without finding any unenclosed literals, the function returns False

--> iff_equivalent(): Function returns ((A>B)&(B>A)) as equivalent of (A=B)

--> implies_equivalent(): Function returns ((!A)|B) as equivalent of (A>B)

--> eliminate_op(): Function eliminates occurrences of a specified operator (op). The function recursively iterates through the expression, identifying instances of the operator and replacing them with their equivalent expressions

--> process_operand(): Function ensures that the operand is properly formatted by eliminating unnecessary parentheses while preserving the outermost parentheses if they exist. It then returns the processed operand without any parentheses

--> split_around_and(): Function splits the expression around the "&" (logical AND) operator, processes the individual operands, and returns a modified list representing the processed expression

--> move_not_inwards(): Function iteratively moves the logical NOT ("!") operator inwards by applying certain transformations to the expression. The goal is to push the NOT operators towards the literals or sub-expressions within parentheses, making the expression more standard

--> distribute_or_over_and(): Function applies the distribution law by distributing the logical OR ("|") operator over logical AND ("&") operators. The goal is to convert expressions with nested ORs and ANDs into a more standardized form

--> eliminate_invalid_parenthesis(): Function removes invalid or unnecessary parentheses by maintaining a stack of content and brackets. The function iterates through the input sentence and adjusts the parentheses



# Part(0) -- Convert each formula into CNF
--> CNF(): Function performs a sequence of transformations, including eliminating specific operators, adjusting parentheses, moving NOT operators inwards, and distributing OR over AND, to convert a logical sentence into Conjunctive Normal Form. The process continues iteratively until no further changes are made. The final step involves splitting the sentence around AND operators to achieve the CNF

--> vet_sentence(): Function ensures proper parenthesization, eliminates invalid or unnecessary parentheses, and returns the sentence in Conjunctive Normal Form (CNF) by calling the CNF function



--> clause_map(): Function returns a map where the keys are literals in the sentence, and the values indicate whether each literal is negated (True for negated, False for non-negated)

--> format_dict(): Function takes a dictionary as input, where keys are literals and values are boolean indicators of whether each literal is negated. It returns a formatted string representation of the dictionary, where negated literals are prefixed with "!"

--> _get_input(): Function to take the input in the format as mentioned in assignment and returns m, list of propositional sentences and query
The first line contains two integer values 'n' and 'm'. The value 'n' denotes the number of formulas in the KB, and 'm' denotes the mode. 
- The next 'n' lines contain one formula per line. 
- The last line contains the query that needs to be proved. 
- There is no space between two consecutive operators/variables




# Part-A
# (1) Implement the resolution-refutation algorithm posing it as an uninformed search problem

--> resolve(): Function implements the resolution algorithm for a given sentence in Conjunctive Normal Form (CNF) and returns True if the sentence is satisfiable and False otherwise. It also provides an option to print the resolution steps based on the mode parameter

--> generate_neighbors(): Function explores neighboring states by identifying clauses connected by the "&" operator in the CNF sentence and attempting to resolve them. It creates new states based on the resolution outcomes and returns a list of these neighboring states

--> resolve_clauses(): Function takes two clauses, represented as strings, and attempts to resolve them. It returns the resolvent if resolution is successful, and None if there is a contradiction, indicating that the clauses cannot be resolved

--> uninformed_search(): Function explores the search space using breadth-first search, applying resolution steps to determine the satisfiability of the knowledge base with the query. If the search reaches a state with an empty clause, it returns 1, indicating unsatisfiability otherwise, it returns 0. The optional mode parameter in the resolve function determines whether to print resolution steps during the search based on the value of input m. Function also calculates the total number of nodes explored and returns it.

--> main(): The script takes input, constructs a knowledge base, and a query, performs an uninformed search, and prints the result with optional resolution steps based on the mode m



# Part-A
# (2) Implement the resolution-refutation algorithm posing it as a greedy search problem

--> heuristic(): Function is a heuristic function used in search algorithms based on the number of literals in a clause. It takes a clause as input and returns an integer representing the count of literals in the clause

--> resolve_greedy(): Function resolves a sentence using a greedy strategy, prioritizing the resolution of clauses with fewer literals based on a heuristic. It provides information about the resolution steps and returns whether the goal state (empty clause) was reached and the total number of explored nodes. The function provides an option to print resolution steps during the process based on the value of m

--> main(): Function takes input, constructs a knowledge base, vetted query, and a resolution input (rub). It then calls the resolve function with the resolution input and prints the result. The result is an integer (0 or 1) indicating whether the resolution was successful. Also prints the total number of nodes explored

