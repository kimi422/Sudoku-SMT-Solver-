# Sudoku-SMT-Solver-
Sudoku solver implemented in Python using the Z3 SMT solver.

# Core Logic of Sudoku Solver: 

X = [[Int(f"x_{r}_{c}") for c in range(9)] for r in range(9)]
s = Solver()

s.add([
    And(1 <= X[r][c], X[r][c] <= 9)
    for r in range(9)
    for c in range(9)
])

s.add([Distinct(X[r]) for r in range(9)])

s.add([
    Distinct([X[r][c] for r in range(9)])
    for c in range(9)
])

s.add([
    Distinct([
        X[3 * br + r][3 * bc + c]
        for r in range(3)
        for c in range(3)
    ])
    for br in range(3)
    for bc in range(3)
])

s.add([
    X[r][c] == puzzle[r][c]
    for r in range(9)
    for c in range(9)
    if puzzle[r][c] != 0
])

s.check()
