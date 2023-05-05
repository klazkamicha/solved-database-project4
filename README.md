Download Link: https://assignmentchef.com/product/solved-database-project4
<br>



Lock Table

<h1>Project Hierarchy</h1>

Project Overview

<ul>

 <li>Your task is to implement a <strong>lock table </strong>module that manages lock objects of multiple threads.</li>

 <li>The module doesn’t need to be compatible with your developing database in this step.</li>

 <li>Instead, the module <strong>should be correctly working with the given test code</strong>.</li>

 <li>This project is a prerequisite step for the next project, Concurrency Control.</li>

 <li>Design your lock table and describe it on hconnect <strong>Wiki </strong></li>

</ul>

Overall Architecture

<strong>(mutex)</strong>

<h1>Overall Architecture</h1>

Lock Table APIs

<h2>int init_lock_table(void)</h2>

<ul>

 <li>Initialize any data structures required for implementing lock table, such as hash table, lock table latch, etc.</li>

 <li>If success, return 0. Otherwise, return non-zero value.</li>

</ul>

<h2>lock_t* lock_acquire(int table_id, int64_t key)</h2>

<ul>

 <li>Allocate and append a new lock object to the lock list of the record having the</li>

 <li>If there is a predecessor’s lock object in the lock list, <strong>sleep </strong>until the predecessor to release its lock.</li>

 <li>If there is no predecessor’s lock object, return the address of the new lock object.</li>

 <li>If an error occurs, return NULL.</li>

</ul>

<h2>int lock_release(lock_t* lock_obj)</h2>

<ul>

 <li>Remove the <em>lock_obj </em>from the lock list.</li>

 <li>If there is a successor’s lock waiting for the thread releasing the lock, <strong>wake up </strong>the successor.</li>

 <li>If success, return 0. Otherwise, return non-zero value.</li>

</ul>

<h1>Lock Table APIs</h1>

Hash Table

<strong>elements</strong>

<h1>Lock List</h1>

lock_acquire()

lock_acquire()

lock_release()

Lock Object




<ul>

 <li>The given test code will</li>

 <li>call <em>init_lock_table() </em>API function,</li>

 <li>create multiple threads each of which</li>

 <li>repeatedly acquire and release multiple record locks by calling <em>lock_acquire()</em>, <em>lock_release()</em>.</li>

 <li>The test code will safely schedule the operations avoiding deadlock, so you <strong>don’t have to deal with the deadlock problem </strong>in this project.</li>

 <li>Analyze the test code as much as you want.</li>

</ul>

<strong>Transfer thread</strong>

0     1     2     3     4     5     6     7                   0     1     2     3     4     5     6     7

<table width="664">

 <tbody>

  <tr>

   <td width="39">77</td>

   <td width="39">-20</td>

   <td width="39">100</td>

   <td width="39">55</td>

   <td width="78">-120 -30</td>

   <td width="39">62</td>

   <td width="76">…</td>

   <td width="39">35</td>

   <td width="39">200</td>

   <td width="39">22</td>

   <td width="39">340</td>

   <td width="39">-123</td>

   <td width="39">-99</td>

   <td width="39">230</td>

   <td width="39">85</td>

  </tr>

 </tbody>

</table>

accounts 230…

table1                                                              table2

<strong>Transfer thread</strong>

0     1     2     3     4     5     6     7                   0     1     2     3     4     5     6     7

<table width="664">

 <tbody>

  <tr>

   <td width="39">77</td>

   <td width="39">-20</td>

   <td width="39">100</td>

   <td width="39">55</td>

   <td width="78">-120 -30</td>

   <td width="39">62</td>

   <td width="76">…</td>

   <td width="39">35</td>

   <td width="39">200</td>

   <td width="39">22</td>

   <td width="39">340</td>

   <td width="39">-123</td>

   <td width="39">-99</td>

   <td width="39">230</td>

   <td width="39">85</td>

  </tr>

 </tbody>

</table>

accounts 230…

table1                                                              table2

<strong>Transfer thread</strong>

0     1     2     3     4     5     6     7                   0     1     2     3     4     5     6     7

<table width="664">

 <tbody>

  <tr>

   <td width="39">77</td>

   <td width="39">-20</td>

   <td width="39">100</td>

   <td width="39">55</td>

   <td width="78">-120 -30</td>

   <td width="39">62</td>

   <td width="76">…</td>

   <td width="39">35</td>

   <td width="39">200</td>

   <td width="39">22</td>

   <td width="39">340</td>

   <td width="39">-123</td>

   <td width="39">-99</td>

   <td width="39">230</td>

   <td width="39">85</td>

  </tr>

 </tbody>

</table>

accounts 230…

table1                                                              table2

<strong>Transfer thread</strong>

0     1     2     3     4     5     6     7                   0     1     2     3     4     5     6     7

<table width="664">

 <tbody>

  <tr>

   <td width="39">77</td>

   <td width="39">-20</td>

   <td width="39"><strong>90</strong></td>

   <td width="39">55</td>

   <td width="78">-120 -30</td>

   <td width="39">62</td>

   <td width="76">…</td>

   <td width="39">35</td>

   <td width="39"><strong>210</strong></td>

   <td width="39">22</td>

   <td width="39">340</td>

   <td width="39">-123</td>

   <td width="39">-99</td>

   <td width="39">230</td>

   <td width="39">85</td>

  </tr>

 </tbody>

</table>

accounts 230…

table1                                                              table2

<strong>Transfer thread</strong>

0     1     2     3     4     5     6     7                   0     1     2     3     4     5     6     7

<table width="664">

 <tbody>

  <tr>

   <td width="39">77</td>

   <td width="39">-20</td>

   <td width="39"><strong>90</strong></td>

   <td width="39">55</td>

   <td width="78">-120 -30</td>

   <td width="39">62</td>

   <td width="76">…</td>

   <td width="39">35</td>

   <td width="39"><strong>210</strong></td>

   <td width="39">22</td>

   <td width="39"><strong>365</strong></td>

   <td width="39">-123</td>

   <td width="39">-99</td>

   <td width="39">230</td>

   <td width="39"><strong>60</strong></td>

  </tr>

 </tbody>

</table>

accounts 230…

table1                                                              table2

<strong>Transfer thread</strong>

0     1     2     3     4     5     6     7                   0     1     2     3     4     5     6     7

<table width="664">

 <tbody>

  <tr>

   <td width="39">77</td>

   <td width="39">-20</td>

   <td width="39"><strong>90</strong></td>

   <td width="39">55</td>

   <td width="78">-120 -30</td>

   <td width="39">62</td>

   <td width="76">…</td>

   <td width="39">35</td>

   <td width="39"><strong>210</strong></td>

   <td width="39">22</td>

   <td width="39"><strong>365</strong></td>

   <td width="39">-123</td>

   <td width="39">-99</td>

   <td width="39">230</td>

   <td width="39"><strong>60</strong></td>

  </tr>

 </tbody>

</table>

accounts 230…

table1                                                              table2

<strong>Scan thread</strong>




Deadline &amp; Regulations

<ul>

 <li>Deadline: <strong>Nov 15 11:59pm</strong></li>

 <li>We’ll only score your commit before the deadline, and your submission after the deadline will not be accepted.</li>

 <li>You must follow the given project hierarchy and the path of the</li>

</ul>

“unittest_lock_table” executable file, otherwise, you cannot get a score.

<h1>Thank you</h1>