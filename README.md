Download Link: https://assignmentchef.com/product/solved-comp3500-lab-1-assignment
<br>
<strong>Objectives of this assignment: </strong>

<ul>

 <li>to work on a Unix based system</li>

 <li>to “<em>dust off</em>” your programming skills in C</li>

 <li>to become familiar with the notion of a process control block</li>

 <li>to experience the life cycle of a process</li>

 <li>to “feel” how an operating system manages processes</li>

 <li>to evaluate and compare three fundamental scheduling policies</li>

</ul>

<strong> </strong>

<strong>IMPORTANT:  </strong>

<ul>

 <li><em>Your code will be tested and graded <strong>REMOTELY </strong>on the Engineering Unix (Tux) machines. If the code does not work on those machines, you will not get any credit even if your code works on any other machine. </em></li>

 <li><em>A late submission will get a 50% penalty if submitted right after the deadline. The next day, you cannot submit the lab. </em></li>

 <li><em>One submission per group. </em></li>

 <li><em>Writing and presentation of your report are considered to grade your lab (30%). Your conclusions <strong>must be supported</strong> by the data/measurements you collect. </em></li>

 <li><em>The quality of your code will be evaluated (20%). </em></li>

 <li><strong><em>Questions about this lab must be posted on Piazza if you need a timely answer</em></strong><em>. </em></li>

</ul>




<strong>Lab Assignment (Turned in by one group mate)  </strong>It is assumed that by 5:00pm May 25, <strong>first</strong>, 1) you have an engineering Unix account, 2) you can edit text files, 3) you can compile C programs, and 4) you can execute C programs on the Unix (Tux) machines. You can use any personal computer or computing lab to remotely access the Engineering Unix (Tux) machines.  <strong>second, </strong>you have your group partners signed up on Canvas: 2 points penalty per day late.







<strong>Look at the “How to get started?” section at the very end of the lab.</strong>

This lab has three parts: 1) Write an efficient code to simulate CPU scheduling policies, 2) evaluate these policies, and 3) analyze and report your results. Efficient code means a code that 1) is correct, , 2) is concise, 3) does not waste memory, and does not waste CPU cycles.




The instructor designed and implemented in C an emulation framework that allows the simulation of processes in order to implement and evaluate different CPU scheduling and memory management strategies.







A process is represented by a Process Control Block defined as follow




typedef struct ProcessControlBlockTag{

Identifier ProcessID;

State      state;

Priority   priority;

Timestamp  JobArrivalTime;   /* Time when job first entered job queue    */

TimePeriod TotalJobDuration; /* Total CPU time job requires              */

TimePeriod TimeInCpu;        /* Total time process spent so far on CPU   */

TimePeriod CpuBurstTime;     /* Length of typical CPU burst of job       */

TimePeriod RemainingCpuBurstTime; /* Remaing time of current CPU burst   */

TimePeriod IOBurstTime;      /* Length of typical I/O burst of job       */

TimePeriod TimeIOBurstDone;  /* Time when current I/O will be done       */

Timestamp  JobStartTime;     /* Time when job first entered ready queue  */

Timestamp  StartCpuTime;     /* Time when job was first placed on CPU    */

Timestamp  TimeEnterWaiting; /* Last time Job Entered the Waiting Queue  */

Timestamp  JobExitTime;      /* Time when job first entered exit queue   */

TimePeriod TimeInReadyQueue; /* Total time process spent in ready queue  */

TimePeriod TimeInWaitQueue;  /* Total time process spent in wait queue   */

TimePeriod TimeInJobQueue;   /* Total time process spent in job queue    */

Memory     TopOfMemory;      /* Address of top of allocated memory block */   Memory     MemorySize;       /* Amount of allocated memory in bytes      */   struct ProcessControlBlockTag *previous; /* previous element in linked list */   struct ProcessControlBlockTag *next;     /* next element in linked list */ } ProcessControlBlock;




The emulation framework can be viewed as follows:




<strong> </strong>

The system consists of two components: a “<strong><em>Processes Generator</em></strong>” and a “<strong><em>Processes Management</em></strong>” system. These two componentsconsist of two C programs: <em>processesgenerator.c</em> and <em>processmanagement.c</em>. In order to facilitate your task, you do not have access to the source of the program <em>processesgenerator.c</em>. You will use only the object file <em>processesgenerator.o </em>provided by the instructor.




Your task is to “complete” the program <em>processesmanagement.c</em>. In order to facilitate your task, the instructor built the template for this program using routines and variables to show you how to use them. You must <em>augment</em> this program (<em>processesmanagement.c</em>) to implement and evaluate three different CPU scheduling policies: first come first serve (<strong>FCFS</strong>), shortest remaining time first (<strong>SRTF</strong>), and Round Robin (<strong>RR</strong>). Your program must implement these strategies and instrument the code to compute and collect the average turnaround time, the average response time, the CPU Busy time (%), the throughput, and the average waiting Time (in <strong>Ready State</strong>). After you collect these averages for each CPU scheduling policy, analyze, compare, and draw conclusions about CPU scheduling. You must implement/complete these routines:

<ul>

 <li>FCFS_Scheduler()</li>

 <li>SRTF_Scheduler()</li>

 <li>RR_Scheduler()</li>

 <li>Dispatcher()</li>

 <li>BookKeeping()dispatch</li>

</ul>




The <em>Processes Generator </em>generates processes with an inter-arrival time exponentially distributed. Whenever a process is generated, the routine <em>NewJobIn</em> (in <strong><em>processesmanagement.c</em></strong>) is called. In order to “start” you, the instructor already included instruction to add every new job to the Job Queue (JOBQUEUE). From this point, you must manage these jobs just like an operating system would do.

You will be provided three files: <strong><em>common.h</em></strong>, <strong><em>processesgenerator.o</em></strong>, and <strong><em>processesmanagement.c</em></strong>. You are not allowed to modify the file <strong><em>common.h</em></strong> or the <strong><em>main</em></strong> function in the <strong><em>processesmanagement.c</em></strong> file. In the file <em>processesmanagement.c</em>, you must develop your code <strong><em>INSIDE</em></strong> the function <strong><em>ManageProcesses(). </em></strong>You may add new global variables or new routines (functions, methods) in the file <em>processesmanagement.c</em>. The instructor indicated on the program the routines/functions you need to implement.




To compile your program,

you must type: <strong><em>cc -o pm processesgenerator.o processesmanagement.c -lm</em></strong> where   <strong><em>processesgenerator.o </em></strong>is the object file that emulates devices generating events   <strong><em>pm </em></strong> is the executable.

<strong><em>processesmanagement.c</em> </strong>is the source file you must “complete”.




<strong>YOU CANNOT MODIFY <em>common.h</em> </strong>(the original file common.h will be used to compile your submitted code) <strong>YOU CAN create new variables, new types, new routines/functions …. in <em>processesmanagement</em>.c . </strong>

<strong> </strong>

2) <strong>Policy Evaluation:  </strong>

<ol>

 <li>Compile your code with “<em>cc –o pm processesgenerators.o processesmanagement.c -lm</em>”.</li>

 <li>Execute your code with “./pm PolicyNumber” where <em>PolicyNumber</em> is the CPU scheduling policy. <em>PolicyNumber </em>must take the value 1, 2, and 3 for FCFS, SRTF, and RR, respectively. <strong><em>The code generates 250 processes and stops. </em></strong></li>

 <li>In order to evaluate your code <strong>for each policy</strong>, you must execute the program until it stops. You must “instrument” your code to collect <strong>for each policy</strong> the average turnaround time (<strong>TAT</strong>), the average response time (<strong>RT</strong>), the CPU Busy time (%) (<strong>CBT</strong>), the throughput (<strong>T</strong>), and the average waiting time (in <strong>Ready State</strong>) (<strong>AWT</strong>).</li>

</ol>

<table width="439">

 <tbody>

  <tr>

   <td width="113"><strong>Policy</strong></td>

   <td width="115"><strong>PolicyNumber</strong></td>

   <td width="48"><strong>TAT</strong></td>

   <td width="36"><strong>RT</strong></td>

   <td width="48"><strong>CBT</strong></td>

   <td width="26"><strong>T</strong></td>

   <td width="54"><strong>AWT</strong></td>

  </tr>

 </tbody>

</table>







<table width="784">

 <tbody>

  <tr>

   <td colspan="9" width="784"></td>

  </tr>

  <tr>

   <td colspan="9" width="784"> </td>

  </tr>

  <tr>

   <td rowspan="9" width="172"> </td>

   <td width="113"><strong>FCFS </strong></td>

   <td width="115"> </td>

   <td width="48"> </td>

   <td width="36"> </td>

   <td width="48"> </td>

   <td width="26"> </td>

   <td width="54"> </td>

   <td rowspan="9" width="172"> </td>

  </tr>

  <tr>

   <td width="113"><strong>SRTF </strong></td>

   <td width="115"> </td>

   <td width="48"> </td>

   <td width="36"> </td>

   <td width="48"> </td>

   <td width="26"> </td>

   <td width="54"> </td>

  </tr>

  <tr>

   <td width="113"><strong>RR (Q=  1 ms) </strong></td>

   <td width="115"> </td>

   <td width="48"> </td>

   <td width="36"> </td>

   <td width="48"> </td>

   <td width="26"> </td>

   <td width="54"> </td>

  </tr>

  <tr>

   <td width="113"><strong>RR (Q=  5 ms) </strong></td>

   <td width="115"> </td>

   <td width="48"> </td>

   <td width="36"> </td>

   <td width="48"> </td>

   <td width="26"> </td>

   <td width="54"> </td>

  </tr>

  <tr>

   <td width="113"><strong>RR (Q= 10 ms </strong></td>

   <td width="115"> </td>

   <td width="48"> </td>

   <td width="36"> </td>

   <td width="48"> </td>

   <td width="26"> </td>

   <td width="54"> </td>

  </tr>

  <tr>

   <td width="113"><strong>RR (Q= 15 ms </strong></td>

   <td width="115"> </td>

   <td width="48"> </td>

   <td width="36"> </td>

   <td width="48"> </td>

   <td width="26"> </td>

   <td width="54"> </td>

  </tr>

  <tr>

   <td width="113"><strong>RR (Q= 20 ms </strong></td>

   <td width="115"> </td>

   <td width="48"> </td>

   <td width="36"> </td>

   <td width="48"> </td>

   <td width="26"> </td>

   <td width="54"> </td>

  </tr>

  <tr>

   <td width="113"><strong>RR (Q= 25 ms </strong></td>

   <td width="115"> </td>

   <td width="48"> </td>

   <td width="36"> </td>

   <td width="48"> </td>

   <td width="26"> </td>

   <td width="54"> </td>

  </tr>

  <tr>

   <td width="113"><strong>RR (Q= 50 ms </strong></td>

   <td width="115"> </td>

   <td width="48"> </td>

   <td width="36"> </td>

   <td width="48"> </td>

   <td width="26"> </td>

   <td width="54"> </td>

  </tr>

 </tbody>

</table>




For Round Robin, you must collect <em>TAT, RT, CBT, T, </em>and<em> AWT</em> for the following values for the quantum: 1 ms, 5 ms, 10 ms, 15 ms, 20 ms, 25 ms, and 50 ms.

For RR, plot <em>TAT, RT, CBT, T, </em>and<em> AWT </em>as a function of the quantum<strong><em>.</em> </strong>




3) <strong>CPU Scheduling Analysis: </strong>

Based on the measurements for the different policies, discuss and compare the different policies (and the impact of the <em>quantum</em> for RR). Do these values match the expected performance of the different policies?

<strong>Get Started </strong>

1) compile the code I provided you by typing: <strong><em> </em></strong>

<h1>cc-o pm processesgenerator.o processesmanagement.c -lm</h1>

2) Execute the code: ./pm 1  3) Observe how the job queue grows 4) Stop the execution with CTRL-C.

<ul>

 <li>Execute: ./pm 1 <strong>1</strong></li>

 <li>Now, with the parameter 1 (highlighted in red), you should see processes generated: the character ‘G’ appears just before displaying the process.</li>

 <li>Stop with CTRL-C…..</li>

 <li>“Play” with code <strong><em>ManageProcesses()</em></strong> in processmanagement.c for detecting all processes, then try to manage them.</li>

</ul>


