Download Link: https://assignmentchef.com/product/solved-comp9024-assignment-3-binomial-heap-based-priority-queue
<br>
In this assignment, you will implement a binomial heap-based priority queue and solve a task scheduling problem using priority queues.

Background

An embedded system is a computer system performing dedicated functions within a larger mechanical or electrical system.  Embedded systems range from portable devices such as Google Glasses, to large stationary installations like traffic lights, factory controllers, and complex systems like hybrid vehicles, and avionic.  Typically, the software of an embedded system consists of a set of tasks (threads) with timing constraints. Typical timing constraints are release times and deadlines. A release time specifies the earliest time a task can start, and a deadline is the latest time by which a task needs to finish.     One major goal of embedded system design is to find a feasible schedule for the task set such that all the timing constraints are satisfied.

Task scheduler

We assume that the hardware platform of the target embedded systems is a single processor with m identical cores, Core1, Core2, …, Corem. The task set V={v<sub>1</sub>, v<sub>2</sub>, …, v<sub>n</sub>} consists of n independent, non-pre-emptible tasks. A non-pre-emptible task cannot be pre-empted by another task during its execution, i.e., it runs to completion without being interrupted.  Each task v<sub>i</sub> (i=1, 2, …, n) has four attributes: a unique task name v<sub>i</sub>, an execution time c<sub>i</sub>, a release time r<sub>i</sub>, and a deadline d<sub>i </sub>(d<sub>i</sub>&gt;r<sub>i</sub>). All the execution times, the release times and deadlines are non-negative integers. You need to design a task scheduler and implement it in C. Your task scheduler uses EDF (Earliest Deadline First) heuristic to find a feasible schedule for a task set. A schedule of a task set specifies when each task starts and on which core it is executed.  A feasible schedule is a schedule satisfying all the release time and deadline constraints.

The problem of finding a feasible schedule for this task scheduling problem is NP-complete. It is widely believed that an NP-complete problem has no polynomial-time algorithm. However, nobody can prove it.

First, we introduce two definitions: scheduling point and ready task.

<ul>

 <li>A scheduling point is a time point at which a task can be scheduled on a core, In other words, a scheduling point is either the release time or the completion time of a task.</li>

 <li>A task v<sub>i</sub> (i=1, 2, …, n) is ready at a time t if t≥r<sub>i</sub></li>

</ul>

The EDF scheduling heuristic works as follows:

<ul>

 <li>At each scheduling point t<sub>i</sub> (t<sub>i</sub>≤t<sub>i</sub>+1, i=1, 2, …), among all the ready tasks, find a task with the smallest deadline, and schedule it on an idle core such that its start time is minimized. Ties are broken arbitrarily.</li>

</ul>

Since this task scheduling problem is NP-complete, the EDF heuristic is not guaranteed to find a feasible schedule even if a feasible schedule exists.

<h1>Example One</h1>

Consider a set S<sub>1</sub> of 6 independent tasks whose release times and deadlines are shown in Table 1. The target processor has two identical cores. A feasible schedule of the task set by using EDF scheduling strategy is shown in Figure 1.

Table 1: A set S<sub>1</sub> of 6 tasks with individual release times and deadlines

<table width="378">

 <tbody>

  <tr>

   <td width="95">Task</td>

   <td width="94">Execution time</td>

   <td width="94">Release time</td>

   <td width="95">Deadline</td>

  </tr>

  <tr>

   <td width="95">v<sub>1</sub></td>

   <td width="94">4</td>

   <td width="94">0</td>

   <td width="95">4</td>

  </tr>

  <tr>

   <td width="95">v<sub>2</sub></td>

   <td width="94">4</td>

   <td width="94">1</td>

   <td width="95">5</td>

  </tr>

  <tr>

   <td width="95">v<sub>3</sub></td>

   <td width="94">5</td>

   <td width="94">3</td>

   <td width="95">10</td>

  </tr>

  <tr>

   <td width="95">v<sub>4</sub></td>

   <td width="94">6</td>

   <td width="94">4</td>

   <td width="95">11</td>

  </tr>

  <tr>

   <td width="95">v<sub>5</sub></td>

   <td width="94">4</td>

   <td width="94">6</td>

   <td width="95">13</td>

  </tr>

  <tr>

   <td width="95">v<sub>6</sub></td>

   <td width="94">5</td>

   <td width="94">6</td>

   <td width="95">18</td>

  </tr>

 </tbody>

</table>




Time       0   1   2   3   4   5   6   7   8    9  10 11 12  13  14 15 16

Figure 1: A feasible schedule for S<sub>1</sub>

<h1>Example Two</h1>

Consider a set S<sub>2 </sub>of 6 independent tasks whose release times and deadlines are shown in Table 2. The target processor has two identical cores. A schedule of the task set by using EDF scheduling strategy is shown in Figure 2. As we can see, in the schedule, v<sub>6</sub> finishes at time 16 and thus misses its deadline. Therefore, the schedule is not feasible. However, a feasible schedule, as shown in Figure 3, does exist.

Table 2: A set of tasks with individual release times and deadlines

<table width="378">

 <tbody>

  <tr>

   <td width="95">Task</td>

   <td width="94">Execution time</td>

   <td width="94">Release time</td>

   <td width="95">Deadline</td>

  </tr>

  <tr>

   <td width="95">v<sub>1</sub></td>

   <td width="94">4</td>

   <td width="94">0</td>

   <td width="95">4</td>

  </tr>

  <tr>

   <td width="95">v<sub>2</sub></td>

   <td width="94">4</td>

   <td width="94">1</td>

   <td width="95">5</td>

  </tr>

  <tr>

   <td width="95">v<sub>3</sub></td>

   <td width="94">5</td>

   <td width="94">3</td>

   <td width="95">10</td>

  </tr>

  <tr>

   <td width="95">v<sub>4</sub></td>

   <td width="94">6</td>

   <td width="94">4</td>

   <td width="95">11</td>

  </tr>

  <tr>

   <td width="95">v<sub>5</sub></td>

   <td width="94">4</td>

   <td width="94">9</td>

   <td width="95">16</td>

  </tr>

  <tr>

   <td width="95">v<sub>6</sub></td>

   <td width="94">5</td>

   <td width="94">10</td>

   <td width="95">15</td>

  </tr>

 </tbody>

</table>




Time       0   1   2   3   4   5   6    7   8    9 10 11  12 13 14 15 16

Figure 2: An infeasible schedule constructed by the EDF scheduling strategy

Time       0   1   2   3   4   5   6   7   8    9  10 11  12 13 14 15 16

Figure 3: A feasible schedule for S<sub>2</sub>

<strong> </strong>The TaskScheduler function

You need to write a task scheduler function named <strong>TaskScheduler</strong>. A prototype of  <strong>TaskScheduler</strong> is shown as follows:

int TaskScheduler(char *file1, char *file2, int m) {};

This function gets a task set from a file named file1, constructs a feasible schedule for the task set on a processor with m identical cores by using the EDF strategy, and writes the feasible schedule to file2.  If a feasible schedule is found, it returns 1. Otherwise, it returns 0.

Both file1 and file2 are text files. file1 contains a set of independent tasks each of which has a name, an execution time, a release time and a deadline in that order. Task names, execution times, release times and the deadlines are a string of digits between 0 and 9.  All the release times are non-negative integers, and all the execution times and the deadlines are natural numbers. The format of file1 is as follows:

v1 c1 r1 d1 v2 c2 r2 d2 … vn cn rn dn

Two adjacent attributes (task name, execution time, release time and deadline) are separated by one or more white space characters or a newline character. A sample file1 is shown <a href="https://www.cse.unsw.edu.au/%7Ehuiw/file1.txt">here</a><a href="https://www.cse.unsw.edu.au/%7Ehuiw/file1.txt">.</a>

For simplicity, you may assume that all the task names in file1 are distinct. Therefore, you don’t need to check for duplicates.

The TaskScheduler function needs to handle the following possible cases properly when reading from file1 and writing to file2:

<ol>

 <li>file1 does not exist. In this case, print “file1 does not exist” and the program terminates.</li>

 <li>file2 already exists. In this case, overwrite the old file2.</li>

 <li>The task attributes (task name, execution time, release time and deadline) of file1 do not follow the formats as shown before. In this case, print “input error when reading the attribute of the task X” and the program terminates, where X is the name of the task with an incorrect attribute.</li>

</ol>

file2 has the following format:

v1 p1 t1 v2 p2  t2  … vn pn tn

where each v<sub>i </sub>(i=1, 2, …, n) is the task name, p<sub>i</sub> is the name of the core where v<sub>i</sub> is scheduled, and t<sub>i</sub> is the start time of the task v<sub>i</sub> in the schedule.  In file2, all the tasks must be sorted in non-decreasing order of start times.  A sample file2 is shown <a href="https://www.cse.unsw.edu.au/%7Ehuiw/file2.txt">here</a><a href="https://www.cse.unsw.edu.au/%7Ehuiw/file2.txt">.</a>




Your task scheduler needs to use binomial heap-based priority queues. A priority queue has a header which stores the number of tasks in the heap and other implementation dependent information. The data type of a heap header is defined as follows:

typedef struct BinomialHeap{

int  size;      // count of tasks in the heap

…                // you need to add additional fields here

} BinomialHeap;

Each node in the heap stores the priority (key) and the attributes of a task. The attributes of a

task include its name, execution time, release time and deadline. For simplicity, we use an integer to denote the name of task.

The data type for heap nodes is defined as follows:

typedef struct HeapNode {           int key; // key of this task  int TaskName; // task name

int Etime; // execution time of the task  int Rtime; // release time of the task                int Dline; // deadline of the task

…             // you need to add additional fields here

} HeapNode;

Therefore, you also need to implement the following functions of a binomial heap-based priority queue:

<ol>

 <li>void Insert(BinomialHeap *T, int k, int n, int c, int r, int d). This function inserts a new task into a heap T, where k, n, c, r and d are the key, name, execution time, release time, and deadline of the task, respectively.</li>

 <li>HeapNode *RemoveMin(BinomialHeap *T). This function removes a task with the smallest key from the heap T and returns the node containing the task.</li>

 <li>int Min(BinomialHeap *T). This function returns the smallest key of all the tasks in the heap T without modifying the heap T.</li>

</ol>

The prototypes of all the above-mentioned function and some other basic functions are included in the template file <strong>MyTaskScheduler.c</strong>.  In addition to the above functions, you may add your own helper functions and fields (variables) to the file MyTaskScheduler.c.

<strong>Note that you must implement a binomial heap-based priority queue. Any other priority queues are not acceptable. </strong>

<h1>Time complexity requirement</h1>

You need to include the time complexity analysis of each function as comments in your program. The time complexity of your scheduler is required to be no higher than O(n*log n), where n is the number of tasks (<strong>Hints: use three binomial heap-based priority queues, one priority queue with release times as keys, one priority queue with deadlines as keys and one priority queue for the scheduling points of all the cores</strong>). There is no specific requirement on space complexity. However, try your best to make your program space efficient.

When analysing the time complexity of your task scheduler, you can assume that the time complexity of each function (insertion, deletion, removeMin and merge) on a binomial heap is O(log n), where n is the number of tasks in the binomial heap.


