Software Engineering note

## Software configuration management(SCM)

- Four aspects
  - Change control 
  - Version control 
  - Building
  - Releasing
- Supported by tools
- Requires expertise and oversight 
- More important on large projects

## tests

- Smoke test (build verification test)
  - 冒烟测试是指对提交测试的软件在进行详细深入的测试之前而进行的预测试，这种预测试的主要目的是暴露导致软件需重新发布的基本功能失效等严重问题。冒烟测试可以由开发人员执行，也可以由测试人员来执行。即，在版本编译后正式提交测试之前由开发人员执行；或开发发布版本后，测试人员在接受这个版本作为正式版本进一步测试前执行。
- Unit test
  - 单元测试又称为模块测试，是针对程序模块（软件设计的最小单位）来进行正确性检验的测试工作。**程序单元**是应用的最小可测试部件。在过程化编程中，一个单元就是单个程序、函数、过程等；对于面向对象编程，最小单元就是方法，包括基类（超类）、抽象类、或者派生类（子类）中的方法。
- Regression test
  - 解决一个问题后的测试，方向是判断新的代码是否引入了新问题。



## Extreme Programming

**Waterfall model**

![image-20190604175734500](note.assets/image-20190604175734500.png)



### Extreme Programming

**Main ideas**

- Don't write much documentation
- Implement features one by one
- Release code frequently
- Work closely with the customer
- Communicate a lot with team members



**Key practices**

- Planning game for requirements
- Test-driven development for design and testing
- Refactoring for design
- Pair programming for development
- Continuous integration for integration





XP is an iterative process

- Iteration = two week cycle (1-3 weeks) 
- Iteration is going to implement set of **user stories** 
  - User story: a feature customers want in the software
  - the smallest amount of information necessary to allow the customer to define a path through the system
- Divide work into tasks small enough to finish in a day 



### Pair programming

- Two programmers work side-by-side at one computer, continuously collaborating on the same design, algorithm, code, and test.
- Periodically switch roles of driver and navigator (<=30min)



### Concepts:

- Story point: unit of measure for expressing the overall size of a user story, feature, or other piece of work. The raw value of a story point is unimportant. What matters are the relative values. 
  - Related to how hard it is and how much of it there is
  - Not related to amount of time or the number of people 
  - Unitless, but numerically-meaningful 

- Ideal time: the amount of time “something” takes when stripped of all peripheral activities 
  - Example: American football game = 60 minutes 

- Elapsed time: the amount of time that passes on the clock to do “something”
  - Example: American football game = 3 hours 

- Velocity: measure of a team’s rate of progress 



### Planning

![image-20190605161909525](note.assets/image-20190605161909525.png)

Programmers only worry about one iteration at a time

- Simplicity: add one feature at a time

### Test

Run program with known inputs, check results



术语区别

Fault: defect, bug

Failure: program behaves unexpectedly during testing

Error: difference between "computed, observed, or measured value or condition" and "true, specified, or theoretically correct value or condition"



##### ASSERTION PATTERNS

State Testing Patterns

- Final State Assertion
  - Most Common Pattern: Arrange. Act. Assert.
- Guard Assertion
  - Assert Both Before and After The Action (Precondition Testing)
- Delta Assertion
  - Verify a Relative Change to the State
- Custom Assertion
  - Encodes Complex Verification Rules



##### PARAMETERIZED TESTS

Parameterized tests需要独占一个测试类

@Parameters



##### Theories

@Theory

@DataPoints





#### Test Driven Development

![image-20190606125606643](note.assets/image-20190606125606643.png)

#### Some tips in test

1. Each test should be independent of each other
2. Any given behaviour should be specified in one and only one test.
3. Correct method signature should be assertEquals(expected,actual)



#### Code Coverage

Code coverage is a measure used to describe the degree to which the source code of a program is executed when a particular test suite runs

- White box testing
- a measure of test quality



#### Mutation Testing

Code coverage cannot ensure test quality=>solution: Mutation Testing







## MEASURING SIZE OF SYSTEM

- Lines of code (Source Lines of Code - SLOC)

- Number of classes, functions, files, etc.

- Function Points

### Measure complexity

- Cyclomatic complexity (Thomas J. McCabe, Sr. in 1976)

> A measure of logical complexity
>
> Tells how many tests are needed to execute every statement of program
>
> ```
> =Number of branches (if, while, for) + 1
> ```
>
> **Test view**
>
> Cyclomatic complexity is the **number of independent paths** through the procedure
>
> Gives an **upper bound on the number of tests** necessary to execute every edge of control graph
>
> **Metrics view**
>
> McCabe found that modules with cyclomatic complexity greater than 10 were hard to test and error prone



- Function points

- Coupling and cohesion

- Many OO-specific metrics (may cover later)



### Measure coupling

**DHAMA’S COUPLING METRIC**

```
ßßModule coupling = 1 / (
 number of input parameters + 
 number of output parameters + 
 number of global variables used + 
 number of modules called + 
 number of modules calling 
) 
```

0.5 is low coupling, 0.001 is high coupling 

**Ca** : Afferent coupling: the number of classes **outside** this module that depend on classes inside this module

**Ce** : Efferent coupling: the number of classes **inside** this module that depend on classes outside this module (Measure interrelationships between classes, 越大越不稳定)

```
Instability = Ce / (Ca + Ce)
```

![image-20190606143128382](note.assets/image-20190606143128382.png)



```
Abstractness = number of abstract classes in module / number of classes in module
```

Abstractness越大，Instability越低



### List of OO metrics(不考)

- Weighted Methods Per Class (WMC)

WMC for a class is the sum of the complexities of the methods in the class

**Possible method complexities** 
1 (number of methods)
Lines of code
Number of method calls
Cyclomatic complexity



- Depth of Inheritance Tree (DIT)

Maximum length from a class to the root of the tree

![image-20190422112851694](note.assets/image-20190422112851694.png)

The deeper a class is in the hierarchy, the more methods it inherits and so it is harder to predict its behavior
The deeper a class is in the hierarchy, the more methods it reuses 
Deeper trees are more complex

- Number of Children (NOC)

Number of immediate subclasses

More children is more reuse

- Coupling between Object Classes (CBO)

Number of other classes to which a class is coupled 

- Response for a Class (RFC)

Number of methods in a class or called by a class

- Lack of Cohesion in Methods (LCOM)

```
=Num_don't_share-instance-Num_shared_instance
```



## Reverse Engineering

Discovering design of an artifact, from lower level to higher level.

#### Activities

- Read documentation • Talk to people

- Look at the code

- Work with the system • Write documentation



#### Read All Code in 1 Hour

- Intent: assess a software system via a brief but intensive code review
- Problem: system is large/varied, unfamiliar
- Solution: read code & document findings (important entities, “code smells”, tests)
- Hints: what to look for?
  - Coding styles/idioms, tests (system and unit)
  - Abstract classes or classes high in hierarchy
  - Large entities, comments

## Test

- Dynamic Analysis
- Static Analysis: 
  - 无需运行程序，用于发现早期bug
  - is done after coding and before executing unit tests
  - Tools: Checkstyle, PMD, FindBugs

### junit

1. 测试类的命名

测试类的命名规则是：被测试类的类名+Test

比如有一个类叫IrgSrhDelegate，那么它的测试类的命名就是IrgSrhDelegateTest

2. 测试用例的命名

测试用例的命名规则是：test+用例方法名称

比如要测试的方法叫updateData，那么测试用例的命名就是testUpdateData

3. 测试包名的命名

test.原包名（eg: test.com.wistrons.util)

#### 

**assert(expected_val, test_val)**



### Defensive Programming:

Making sure that no warning produced by Static Analysis is a form of defensive programming

- Redundant code(多余代码) is incorporated to check system state after modifications. 
- Implicit assumptions (隐式假设) are tested explicitly. 
- Risky programming constructs are avoided. 
  - Pointers
  - Dynamic memory allocation
  - Floating-point numbers
  - Parallelism
  - Recursion
  - Interrupts



### Maintenance

#### Fault Tolerance



### Security

Authentication: establishes the identity of an agent

Authorization: establishes what an authenticated agent may do



### Levels of Software Testing

![image-20190606182201150](note.assets/image-20190606182201150.png)

- Unit Test
  - Test individual units of a software
  - A unit: smallest testable part of an application
    - Eg: method
- Integration testing:
  - Verify software quality by testing two or more dependent software modules as a group.
- Big-bang Integration Testing
  - All component are integrated together at once
  - ![image-20190606182746486](note.assets/image-20190606182746486.png)
- Incremental Integration Testing
  - Develop a functional "skeleton" system, Design, code, test, debug a small new piece, Integrate this piece with the skeleton
  - ![image-20190606182805837](note.assets/image-20190606182805837.png)

![image-20190606182959480](note.assets/image-20190606182959480.png)





## System reuse





## UI design

![image-20190606175812843](note.assets/image-20190606175812843.png)



## Comments

### Javadoc

Javadoc comments should be written for **programmers who want to use your code**

**Requirement:**

- Javadoc comments should describe exactly how to use the class, method, constructor 
- Javadoc comments should not describe the internal workings of the class or method (unless it affects the user in some way) 
- javadoc method comments should not tell who uses the method 



#### Tags

![image-20190606180617417](note.assets/image-20190606180617417.png)

#### Rules for writing summaries

![image-20190606180712353](note.assets/image-20190606180712353.png)



# Devops&CI

**Devops:**

Development+ IT Operations(IT运维技术人员)



### Continuous Integration(CI)

![image-20190606181140426](note.assets/image-20190606181140426.png)

#### Automate the build

**Daily build**: Compile working executable on a daily basis

![image-20190606181541535](note.assets/image-20190606181541535.png)



#### Make your build self-testing

**Automated tests**: Tests that can be run from the command line



#### Daily Commits

![image-20190606181852134](note.assets/image-20190606181852134.png)

#### CI Server

An external machine that automatically pulls your latest repo code and fully builds all resources.

- If anything fails, contacts your team (e.g. by email).
- Ensures that the build is never broken for long.



#### Continuous Integration &  Continous Delivery & 

![image-20190606183120245](note.assets/image-20190606183120245.png)

##### Continous Delivery

- Continous Delivery=CI+ automated test suite
- Not every change is a release
  - Manual trigger
  - Trigger on a key file (version)
  - Tag releases!

##### Continuous Deployment

Continuous Deployment=CD+ automatic deployment



# Security Engineering

## Risks type

1. Insecure data storage
2. Weak Server side controls
3. Insufficient transport layer protection
4. Poor Authentication and Authorization
5. Improper Session Handling
