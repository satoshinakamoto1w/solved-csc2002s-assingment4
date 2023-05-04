Download Link: https://assignmentchef.com/product/solved-csc2002s-assingment4
<br>
<strong><em>Concurrent Programming: Tree Growth Simulation </em></strong>

<strong> </strong>

In this assignment, you will design a multithreaded Java program, ensuring both thread safety and sufficient concurrency for it to function well. This is an extension of the parallel computing solution that you developed in the first assignment.

<strong> </strong><strong> </strong><strong> </strong>

<h1>1.   Problem           Description</h1>

<strong>     </strong>

You will implement a multithreaded tree growth simulator (Fig.1).







<em>Figure 1.  The main GUI window for the tree simulator. Note that this mockup is missing the required year counter.  </em>




The user interface to display the results of this simulation should have the following behaviour:

<ul>

 <li>A main display window that draws the trees as rectangles in different shades of green at correct locations in the panel. Trees are drawn in layers (all trees with an extent of [0,2) meters, then [2, 4), and so on). In this way larger trees occlude smaller trees.</li>

 <li>A counter that displays the number of years (generations) since the start of the</li>

</ul>

simulation. Note that this is not shown in Fig. 1.

<ul>

 <li>A ‘reset’ button that sets the extent of all trees to a value of 0.4 and the year count to 0, representing a forest of saplings.</li>

 <li>A ‘pause’ button that temporarily stops the simulation.</li>

 <li>A ‘play’ button that either starts the simulation or allows it to continue running if it was previously paused.</li>

 <li></li>

</ul>

<table>

 <tbody>

  <tr>

   <td width="235"></td>

  </tr>

  <tr>

   <td></td>

   <td></td>

  </tr>

 </tbody>

</table>

<ul>

 <li>An ‘end’ button that closes the window and exits the program.</li>

</ul>

<table>

 <tbody>

  <tr>

   <td width="17"></td>

  </tr>

  <tr>

   <td></td>

   <td></td>

  </tr>

 </tbody>

</table>










<em>Figure 2.  Sunlight simulation for two trees (T1, T2) in different layers. (Left) growth and shading calculations for T1, which takes place first because its larger extent puts it in a layer that is calculated earlier. (Right) T2 has reduced access to sunlight since it is in the shade of T1 and will grow less. </em>




A single generation of simulation (a year) should operate as follows (see Fig. 2):

<ul>

 <li>Trees have a center position (which is where their trunk is located) and an extent (a span to either side of this central position). Thus, the trees in Fig. 2 are T1: (x, y) = (2, 2); extent = 2 and T2: (x, y) = (2,3); extent = 1, assuming that the top-left corner is (0, 0). Note that this is different from the representation in the first assignment, where T1 would be labelled as (x, y) = (0, 0); extent = 5.</li>

 <li>Simulation takes place in layers. First all trees with extent in the range [18, 20), then [16, 18), and so on down to [0, 2). This simulates larger trees dominating smaller trees in the forest as they compete for resources. The order in which trees grow and cast shade within a layer is unimportant. However, a tree must have mutually exclusive access to a given sunlight cell when being simulated to avoid race conditions. For example, if T3 has extent 16.5 and T4 has extent 17.2 they could be simulated in either order (because both are in the [16, 18) layer), but if they overlapped one would need to have its calculations completed before the other was allowed to start.</li>

 <li>At the individual tree level simulation takes place in 3 steps:

  <ol>

   <li>Calculate the average sunlight (s) in the cells that the tree covers.</li>

   <li>Reduce the sunlight in these cells to 10% of their original value. Thus, trees in later layers will receive less sunlight. This simulates the filtering of sunlight through the canopy in a forest.</li>

   <li>A tree then grows in proportion to the average sunlight divided by a factor of 1000: newextent = extent + s / 1000.</li>

  </ol></li>

</ul>




You are provided with skeleton code for the assignment (package treeGrow). When executed, this skeleton provides an incomplete GUI interface with none of the buttons. It will display the initial state of the forest but does not include any simulation. You must build on the skeleton, improving, adding threading and ensuring thread safety when necessary.  You must use appropriate synchronization and your solution should allow for maximal concurrency: operations should not be serialized unless necessary.

<h1>2.   Requirements</h1>




<h2>2.1  Input</h2>




Your program must take a single command-line parameter:  &lt;intput_file&gt;

This encodes data for the landscape and initial forest in the same format as used for the first assignment. You may reuse any code that you developed for loading such files.




<h2>2.2  Controls</h2>




Your program needs to have a reset, pause, play, and end button to control the state of the forest and simulation. There also needs to be a display of the current year. None of this functionality is available in the skeleton.

<strong> </strong><strong> </strong><strong> </strong>

<h2>2.3  Output</h2>




The GUI needs to display the results of the simulation as it occurs. Ideally, the rendering of the forest should occur at a faster rate than the simulation to ensure that none of the detail is missed by the user




<h2>2.4  Code        Architecture</h2>




When extending the code, you are expected to follow the Model-View-Controller pattern (shown in Fig. 3) for user interfaces.  This very common pattern for software architecture separates the internal representation of the information from the display of the information to the user.







<em>Fig. 3. The Model-View-Controller pattern has a clear separation between the display of the information (model) and its internal representation. </em>




In this case, the model comprises the classes such as Land and Tree. The view is the GUI and the controllers will be the threads that you add to alter the model and the view, such as the simulation engine.













<h1>3.   Submission</h1>




<h2>3.1  Report</h2>




You need to write a concise report detailing and explaining the coding you have done.   The report must contain:

<ul>

 <li>A description of each of the classes you added and any modifications you made to the existing classes.</li>

 <li>A description of all the Java concurrency features you used and why they were necessary (e.g. atomic variables, synchronized classes, synchronized collections, barriers etc.).</li>

 <li>You will need to explain how you wrote the code to ensure:

  <ol>

   <li>thread safety (for both shared variables and the Swing library). You should describe when you need to protect data and when you don’t – and explain why.</li>

   <li>Thread synchronization where necessary</li>

   <li>liveness no deadlock.</li>

  </ol></li>

 <li>An explanation of how you validated your system and checked for errors (esp. race conditions).</li>

 <li>An explanation of how your design conforms to the Model-View-Controller pattern.</li>

 <li>Any additional features/extensions to (or improvements on) the basic simulation that you think merit extra credit. There are many things that you can do to improve this simulation.</li>

</ul>


