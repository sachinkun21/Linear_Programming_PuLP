### Linear Programing (LP) is a Powerful Modeling Tool for Optimization:

#### Optimization method using a mathematical model whose requirements are linear relationships.
#### There are 3 BasicComponents in LP:
- Decision Variables - ***what you can control***
- Objective Function - ***math expression that uses variables to express goal***
- Constraints - ***math expression that describe the limits of a solutions***


Use LP to decide on an exercise routine to burn as many calories as possible.
          
                  Pushup                 Running
   
      Calories:  3 per pushup           130 per mile RUN
   
      Minutes:  0.2 per pushup          10 Minutes per mile
 
Constraint - only 10 minutes to exercise

#### Let's Model this problem using LP:
- Decision Variables - What we can control:

      Number of Pushups & Number of Miles Ran
- Objective Function - Math expression that uses variables to express goal:

      - Max (3 * Number of Pushups + 130 * Number of Miles)
- Constraints - Math expression that describe the limits of a solutions:

      1. 0.2 * Number of Pushups + 10 * Number of Miles ≤ 10
      2. Number of Pushups ≥ 0
      3. Number of Miles ≥ 0
      
      
      
      
      
### LP vs IP vs MIP
          Terms                                   Decision Variables
          
          Linear Programing (LP)                  Only Continuous
          Integer Programing (IP)                 Only Discrete or Integers
          Mixed Integer Programing (MIP)          Mix of Continuous and Discrete
          
          
          
## What is PuLP?
- PuLP is a modeling framework for Linear (LP) and Integer Programing (IP) problems written in
Python 
- Maintained by COIN-OR Foundation (Computational Infrastructure forOperations Research)
- PuLP interfaces with Solvers
                    1. CPLEX
                    2. COIN
                    3. Gurobi
                     etc…
                     
   
## PuLP example – resource scheduling
Consultant for boutique cake bakery that sell 2 types of cakes
- 30 day month
- There is:

          - 1 oven
          - 2 bakers
          - 1 packaging packer – only works 22 days      
          
          
- Different resource needs for the 2 types of cakes:

                    Cake A              Cake B
          Oven      0.5 days            1 day
          Bakers    1 day               2.5 days
          Packers   1 day               2 days
              
          Cost      $20.00              $40.00
          
          
### Objective is to Maximize Prot:
          obj = 20*A + 40*B
          
### Constraints: 
          Subject to:
          A ≥ 0
          B ≥ 0
          0.5A + 1B ≤ 30
          1A + 2.5B ≤ 60
          1A + 2B ≤ 22
          
          
### Common modeling process for PuLP
1. Initialize Model
2. Define Decision Variables
3. Define the Objective Function
4. Define the Constraints
5. Solve Model


#### 1. Initialize Model:
          from pulp import *
          
          # Initialize Class
          model = LpProblem("Maximize Bakery Profits", LpMaximize)
#### 2. Define decision variables - LpVariable():
          LpVariable(name, lowBound=None, upBound=None, cat='Continuous', e=None)
          
- name = Name ofthe variable used in the output .lp le
- lowBound = Lower bound
- upBound = Upper bound
- cat = The type of variable this is:

         - Integer
         - Binary
         - Continuous (default)
- e = Used for column based modeling

##### Defining Decision Variables:
          A = LpVariable('A', lowBound=0, cat='Integer')
          B = LpVariable('B', lowBound=0, cat='Integer')

#### 3. Define Objective Function:
          model += 20 * A + 40 * B
          
          Define Constraints
#### 4. Defining Constraints:
          model += 0.5 * A + 1 * B <= 30
          model += 1 * A + 2.5 * B <= 60
          model += 1 * A + 2 * B <= 22
          
          
#### 5. Solve Model:
          model.solve()
          print("Produce {} Cake A".format(A.varValue))
          print("Produce {} Cake B".format(B.varValue))
          
          
          
### FULL CODE: PuLP example – resource scheduling
          
          from pulp import *
          # Initialize Class
          model = LpProblem("Maximize Bakery Profits ,LpMaximize)
          
          # Define Decision Variables
          A = LpVariable('A', lowBound=0, cat= 'Integer')
          B = LpVariable('B', lowBound=0, cat='Integer')
          
          # Define Objective Function
          model += 20 * A + 40 * B
          
          # Define Constraints
          model += 0.5 * A + 1 * B <= 30
          model += 1 * A + 2.5 * B <= 60
          model += 1 * A + 2 * B <= 22
          
          # Solve Model
          model.solve()
          print("Produce {} Cake A".format(A.varValue))
          print("Produce {} Cake B".format(B.varValue))
          
          
### Summary         
- PuLP is a Python LP / IP modeler used to solve Optimization Problems.
- Reviewed: 5 Steps of PuLP modeling process
1. Initialize Model
2. Define Decision Variables
3. Define the Objective Function
4. Define the Constraints
5. Solve Model
Completed Resource Scheduling Example
