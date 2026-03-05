# ADA-LAB-ASSIGNMENT
import time
import matplotlib.pyplot as plt
import sys
# ---------------- FACTORIAL ----------------

fact_calls = 0
def factorial(n):
    global fact_calls
    fact_calls += 1
    if n == 0 or n == 1:
        return 1
    return n * factorial(n - 1)

# ---------------- FIBONACCI RECURSIVE ----------------

fib_rec_calls = 0
def fib_recursive(n):
    global fib_rec_calls
    fib_rec_calls += 1
    if n <= 1:
        return n
    return fib_recursive(n - 1) + fib_recursive(n - 2)


# ---------------- FIBONACCI DP ----------------

fib_dp_calls = 0
def fib_dp(n):
    global fib_dp_calls
    fib_dp_calls += 1
    if n <= 1:
        return n
    dp = [0, 1]
    for i in range(2, n + 1):
        dp.append(dp[i - 1] + dp[i - 2])
    return dp[n]

# ---------------- INPUTS ----------------

inputs = [5, 10, 15]
fact_calls_list = []
fact_time_list = []
fact_space_list = []

fib_rec_calls_list = []
fib_rec_time_list = []
fib_rec_space_list = []

fib_dp_calls_list = []
fib_dp_time_list = []
fib_dp_space_list = []

print("Task 3: Recursion vs Optimized Comparison\n")
print("Algorithm\tInput\tCalls\tTime\t\tSpace (approx stack/list size)")

for n in inputs:

    # -------- Factorial --------
    fact_calls = 0
    start = time.time()
    factorial(n)
    fact_time = time.time() - start

    fact_calls_list.append(fact_calls)
    fact_time_list.append(fact_time)

    # Recursive stack depth ~ n
    fact_space_list.append(n)

    print(f"Factorial\t{n}\t{fact_calls}\t{fact_time:.6f}\t{n}")


    # -------- Fibonacci Recursive --------
    fib_rec_calls = 0
    start = time.time()
    fib_recursive(n)
    fib_rec_time = time.time() - start

    fib_rec_calls_list.append(fib_rec_calls)
    fib_rec_time_list.append(fib_rec_time)

    # Stack depth ~ n
    fib_rec_space_list.append(n)

    print(f"Fib Recursive\t{n}\t{fib_rec_calls}\t{fib_rec_time:.6f}\t{n}")


    # -------- Fibonacci DP --------
    fib_dp_calls = 0
    start = time.time()
    fib_dp(n)
    fib_dp_time = time.time() - start

    fib_dp_calls_list.append(fib_dp_calls)
    fib_dp_time_list.append(fib_dp_time)

    # DP list size ~ n
    fib_dp_space_list.append(n)

    print(f"Fib DP\t\t{n}\t{fib_dp_calls}\t{fib_dp_time:.6f}\t{n}")

    print("-" * 70)


# ---------------- FUNCTION CALL GRAPH ----------------

plt.figure()
plt.plot(inputs, fact_calls_list, label="Factorial Calls")
plt.plot(inputs, fib_rec_calls_list, label="Fibonacci Recursive Calls")
plt.plot(inputs, fib_dp_calls_list, label="Fibonacci DP Calls")
plt.xlabel("Input Size (n)")
plt.ylabel("Number of Function Calls")
plt.title("Function Calls Comparison")
plt.legend()
plt.grid(True)
plt.show()


# ---------------- EXECUTION TIME GRAPH ----------------

plt.figure()
plt.plot(inputs, fact_time_list, label="Factorial Time")
plt.plot(inputs, fib_rec_time_list, label="Fibonacci Recursive Time")
plt.plot(inputs, fib_dp_time_list, label="Fibonacci DP Time")
plt.xlabel("Input Size (n)")
plt.ylabel("Execution Time (seconds)")
plt.title("Execution Time Comparison")
plt.legend()
plt.grid(True)
plt.show()


# ---------------- SPACE COMPLEXITY GRAPH ----------------

plt.figure()
plt.plot(inputs, fact_space_list, label="Factorial Space O(n)")
plt.plot(inputs, fib_rec_space_list, label="Fib Recursive Space O(n)")
plt.plot(inputs, fib_dp_space_list, label="Fib DP Space O(n)")
plt.xlabel("Input Size (n)")
plt.ylabel("Space Usage (Stack depth / DP size)")
plt.title("Space Complexity Comparison")
plt.legend()
import time
import matplotlib.pyplot as plt
import math
# ----------- Recurrence: T(n) = T(n/2) + n -----------
count_a = 0
def recur_a(n):
    global count_a
    count_a += 1
    if n <= 1:
        return 1
    return recur_a(n//2) + n
# ----------- Recurrence: T(n) = 2T(n/2) + n -----------
count_b = 0
def recur_b(n):
    global count_b
    count_b += 1
    if n <= 1:
        return 1
    return recur_b(n//2) + recur_b(n//2) + n
# ----------- Input sizes -----------

sizes = [8, 16, 32, 64]
calls_a, time_a, space_a = [], [], []
calls_b, time_b, space_b = [], [], []
print("\nTask 4 : Recurrence Relation Study\n")
print("Relation\t\t n\tCalls\tTime(sec)\tDepth")
for n in sizes:

    # ----- First recurrence -----
    count_a = 0
    start = time.perf_counter()
    recur_a(n)
    t_a = time.perf_counter() - start
    depth = int(math.log2(n))
    calls_a.append(count_a)
    time_a.append(t_a)
    space_a.append(depth)

    print(f"T(n)=T(n/2)+n\t {n}\t{count_a}\t{t_a:.6f}\t{depth}")
    # ----- Second recurrence -----
    count_b = 0
    start = time.perf_counter()
    recur_b(n)
    t_b = time.perf_counter() - start

    calls_b.append(count_b)
    time_b.append(t_b)
    space_b.append(depth)

    print(f"T(n)=2T(n/2)+n\t {n}\t{count_b}\t{t_b:.6f}\t{depth}")
    print("-"*70)
# ----------- Recursive Calls Graph -----------
plt.figure()
plt.plot(sizes, calls_a, marker='o', label="T(n)=T(n/2)+n")
plt.plot(sizes, calls_b, marker='o', label="T(n)=2T(n/2)+n")
plt.xlabel("Input Size")
plt.ylabel("Total Recursive Calls")
plt.title("Comparison of Recursive Calls")
plt.legend()
plt.grid(True)
plt.show()
# ----------- Time Graph -----------
plt.figure()
plt.plot(sizes, time_a, marker='o', label="T(n)=T(n/2)+n")
plt.plot(sizes, time_b, marker='o', label="T(n)=2T(n/2)+n")
plt.xlabel("Input Size")
plt.ylabel("Execution Time")
plt.title("Time Taken by Recurrences")
plt.legend()
plt.grid(True)
plt.show()
# ----------- Space Graph -----------
plt.figure()
plt.plot(sizes, space_a, marker='o', label="Space for T(n)=T(n/2)+n")
plt.plot(sizes, space_b, marker='o', label="Space for T(n)=2T(n/2)+n")
plt.xlabel("Input Size")
plt.ylabel("Recursion Depth")
plt.title("Space Complexity (Recursion Depth)")
plt.legend()
plt.grid(True)
plt.show()


import time
import matplotlib.pyplot as plt
import tracemalloc

#time Complexity Functions

def constant_time(n):
    return n * 2


def linear_time(n):
    s = 0
    for i in range(n):
        s += i
    return s


def quadratic_time(n):
    s = 0
    for i in range(n):
        for j in range(n):
            s += i + j
    return s


def logarithmic_time(n):
    while n > 1:
        n //= 2


input_sizes = [10, 100, 500, 1000]


#Measuring Time
def measure_time(func, n):
    start = time.time()
    func(n)
    return time.time() - start


#Measuring Space
def measure_space(func, n):
    tracemalloc.start()
    func(n)
    current, peak = tracemalloc.get_traced_memory()
    tracemalloc.stop()
    return peak  # peak memory usage


o1_time, on_time, on2_time, ologn_time = [], [], [], []
o1_space, on_space, on2_space, ologn_space = [], [], [], []


for n in input_sizes:
    o1_time.append(measure_time(constant_time, n))
    on_time.append(measure_time(linear_time, n))
    on2_time.append(measure_time(quadratic_time, n))
    ologn_time.append(measure_time(logarithmic_time, n))

    o1_space.append(measure_space(constant_time, n))
    on_space.append(measure_space(linear_time, n))
    on2_space.append(measure_space(quadratic_time, n))
    ologn_space.append(measure_space(logarithmic_time, n))


#Plotting Time Complexity
plt.figure()
plt.plot(input_sizes, o1_time, marker='o', label="O(1)")
plt.plot(input_sizes, on_time, marker='o', label="O(n)")
plt.plot(input_sizes, on2_time, marker='o', label="O(n²)")
plt.plot(input_sizes, ologn_time, marker='o', label="O(log n)")

plt.xlabel("Input Size (n)")
plt.ylabel("Execution Time (log scale)")
plt.title("Time Complexity Comparison")
plt.legend()
plt.yscale("log")
plt.grid(True)
plt.show()


#Plotting Space Complexity
plt.figure()
plt.plot(input_sizes, o1_space, marker='o', label="O(1)")
plt.plot(input_sizes, on_space, marker='o', label="O(n)")
plt.plot(input_sizes, on2_space, marker='o', label="O(n²)")
plt.plot(input_sizes, ologn_space, marker='o', label="O(log n)")

plt.xlabel("Input Size (n)")
plt.ylabel("Memory Usage (bytes)")
plt.title("Space Complexity Comparison")
plt.legend()
plt.grid(True)
plt.show()

plt.grid(True)
plt.show()
