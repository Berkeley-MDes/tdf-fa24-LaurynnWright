# DES INV 202 Weekly Progress Reports
Lauryn Wright's Journey through Technology Design Foundations 

## Outline
[week 1](README.md#week-1-report-1)

[week 2](https://github.com/Berkeley-MDes/tdf-fa24-LaurynnWright?tab=readme-ov-file#week-2-report-2)

[week 3](https://github.com/Berkeley-MDes/tdf-fa24-LaurynnWright/blob/main/README.md#week-3-report-3)

[week 4](https://github.com/Berkeley-MDes/tdf-fa24-LaurynnWright/blob/main/README.md#week-4-report-4)

[week 5](https://github.com/Berkeley-MDes/tdf-fa24-LaurynnWright/blob/main/README.md#week-5-report-5)

[week 6](https://github.com/Berkeley-MDes/tdf-fa24-LaurynnWright/blob/main/README.md#week-6-report-6)

---
## Week 6: Report 6 #
### 10/04/2024 - 10/10/2024

This week I learned about the Stemma-QT module. I soldered for the first time in order to secure the pins on the Stemma-QT interface board. I then downloaded the provided project files and began to experiment with the acceleration/ gyroscopic sensor. After compiling and flashing the code successfully, the serial monitor produced the following values.
<p align="center"><img width="95%" alt="Accel_Gyro Serial Monitor" src="assets/accel_gyro serial monitor.png"></p>

I decided to install a serial plotter extension to better visualize the output values, and I modified the code to work with the serial plotter. The updated code and plot are shown below. For this data set, the sensor was at rest on a table. The table of variables shows the range of values for the acceleration in the x, y, and z directions and the angular velocity values in the x, y, and z directions.
<p align="center"><img width="95%" alt="Accel_Gyro Initial Plot Code" src="assets/accel_gyro serial monitor.png"></p>
<p align="center"><img width="95%" alt="Accel_Gyro Initial Plot" src="assets/accel_gyro plot.png"></p>
<p align="center"><img width="95%" alt="Accel_Gyro Initial Plot Variables" src="assets/accel_gyro plotter variables.png"></p>

As shown, the values are not centered on zero despite the sensor being at rest, which suggests a need for calibration. I updated the code again so that the plot, while at rest, would center around zero. The photos below show the updated code to zero the data along with a plot of output values. For this plot, the sensor was at rest on a table again. 

While this plot is improved in relation to zeroing the data, it is still demonstrating a lot of noise. I decided to average a span of values rather than plotting every output in an attempt to smooth the curves, minimize the noise, and filter the data. I updated the loop so that a range of values were averaged before that averaged value was plotted. The results of the updated code refined the values, which allowed me to zero the data more accurately. Once I adjusted the offset values, I ran the code again. The updated code and results are shown below. While offering improvement, there are still outliers that could be removed with potentially a low pass or high pass filter.

I also worked with my project-2 team to create a proposal. The following quote from the introduction and objective section of our project proposal outlines our goals for the upcoming week.

> "The goal of this project is to explore the use of **Particle Photon 2 devices**, **Particle Cloud Services**, **Max MSP**, **Touch Designer**, and **STEMMA QT-based sensors and actuators** to develop a **context-aware, interactive jellyfish display**. This feasibility study will evaluate the potential of Particle Photon 2 in an integrated ecosystem, focusing on the reliability of sensor inputs and system responses.
The jellyfish display will respond to physical-touch and distance cues using **Particle Cloud integration** with **Max MSP** prompting audible responses and **Touch Designer** facilitating visual responses. The display will be comprised of two parts: a mechanical jellyfish and a digital interface display. The audiovisual responses will be influenced by user interaction with **force sensitive resistors**, **ultrasonic distance sensors**, and **gesture recognition sensors**. This project emphasizes the integration of physical and digital systems to create a responsive proof of concept. The purpose of the project is to explore how technology can inspire new forms of artistic expression. By integrating sensor-based interactions, this technology can be applied in diverse contexts, such as education, interactive gaming, or as an instrument for creative expression."
>
The image below shows the draft system architecture for our jellyfish project, outlining the key components.
<p align="center"><img width="75%" alt="Jellyfish Draft System Architecture" src="assets/jellyfish draft system architecture1.png"></p>

The following process diagram demonstrates how information is expected to flow between components.
<p align="center"><img width="95%" alt="Jellyfish Process Diagram" src="assets/jellyfish process diagram.png"></p>

---
## Week 5: Report 5 #
### 09/27/2024 - 10/03/2024

This week, I began to familiarize myself with VS Code and the Photon2 microcontroller. In particular, I practiced manipulating the example files created by Jeff Lubow. I went through 5 files (01_helloworld, 02_helloworld_spell, 03_altering_periodicity, 04_make_it_blink, and 05_make_it_blink_outside), each of which are discussed below. 

The **first file**, 01_helloworld, is displayed below. After I initially tried to compile the file, the task failed, so I needed to analyze the error. I noticed that I had forgotten a semicolon on one line, and once I fixed it, the code compiled successfully.
<p align="center"><img width="95%" alt="01_helloworld flashed" src="assets/helloworldcompiledsuccessfully.png"></p>

After compiling the code, I flashed it to my device (Photon2), which was also successful as shown in the screenshot below.
<p align="center"><img width="95%" alt="01_helloworld flashed" src="assets/code01flashedsuccessfullyzoomed.png"></p>

The result of this code is displayed in the serial monitor. Every three seconds, the number of characters in the hello-world message is displayed.
<p align="center"><img width="95%" alt="01_helloworld output" src="assets/code01outputzoomed.png"></p>


In the **second file**, 02_helloworld_spell, the code was changed so that "hello world" is spelled out letter by letter vertically. The code is shown in the screenshot below. The loop works to index each letter in the message as it iterates, relying on "count++" to progress to the next letter. 
<p align="center"><img width="95%" alt="02_helloworld_spell" src="assets/helloworld02compiledsuccessfully.png"></p>

I again compiled the code and flashed it to my device. The serial monitor's output is shown here.
<p align="center"><img width="95%" alt="02_helloworld_spell output" src="assets/code02outputzoomed.png"></p>


The **third file**, 03_altering_periodicity, builds upon the previous file. As "Hello World!" is spelled out vertically, it experiences a specific time delay between each letter. This time delay is also displayed in the serial monitor alongside the letters. An interrupt is used to allow for a button to prompt a change in the time delay. The successfully compiled and flashed code is shown in the photo below.
<p align="center"><img width="95%" alt="03_altering_periodicity" src="assets/code03flashedsuccessfully.png"></p>

For this code to work as intended, I needed to construct the associated circuit. I used the circuit diagram below (left) provided by Jeff Lubow to construct my own circuit (right). The button receives power from the 3V port on the Photon2, and the output feeds into D2. When the button is pressed, it triggers the interupt, which allows for a new periodicity to be used.
<p align="center"><img width="40%" alt="Circuit Diagram" src="assets/microelectronics_intro.png">
<img width="35%" alt="Assembled Circuit" src="assets/assembledbreadboard.jpg"></p>

The circuit worked properly, and the result in the serial monitor is shown below. As seen, the time interval changes after the "Button pressed!" notification appears. Before the notification the displayed interval is 749 ms. Afterward, it is 541 ms.
<p align="center"><img width="95%" alt="03_altering_periodicity output" src="assets/code03outputzoomed.png"></p>


The **fourth file**, 04_make_it_blink, continues to build upon file three. It adds a few lines including lines 44-46 to make the built-in LED on the Photon2 blink. "HIGH" turns on the LED, and "LOW" turns it back off. The loop section of the code is shown below.
<p align="center"><img width="95%" alt="04_make_it_blink" src="assets/code04compiledsuccessfullyzoomed.png"></p>

The output in the serial monitor continues as with file three.
<p align="center"><img width="95%" alt="04_make_it_blink output" src="assets/code04outputzoomed.png"></p>

Below, you can see the built-in LED on the Photon2. It is designated as D7 on the device and in the code.
<p align="center"><img width="95%" alt="Circuit Response" src="assets/breadboard&arrow.jpg"></p>


The **last file** I examined was 05_make_it_blink_outside. This file continued to build on the previous ones and added a command for another external LED to blink alongside the built-in one. The code below shows the input variables. The built-in LED is D7, and the other external LED must connect to D3. The loop is also displayed, and lines 47-51 feature the update. This allows both built-in and external LEDs to blink.
<p align="center"><img width="95%" alt="05_make_it_blink_outside" src="assets/code05flashedsuccessfullyzoomed.png">
 <img width="95%" alt="05_make_it_blink_outside" src="assets/code05zoomed.png"></p>

The resulting output both on the circuit board and in the serial monitor are captured in the video below. "Hello World!" continues to be spelled out vertically in the serial monitor with time intervals changes corressponding to button presses. On the breadboard, the Photon2 light and the LED on the breadboard blink in unison.
<p align="center"> Click the image below to watch the video.
<a href="http://www.youtube.com/watch?feature=player_embedded&v=uQQzzyF3U2A" target="_blank">
 <img src="assets/videothumbnail.png" alt="Watch the video" width=95% />
</a></p>

After working through the files above, I reviewed several of the tutorials listed on the TDF wiki page. I noticed that the LED pulse tutorial was actually incorporated into the code of the earlier files, and the circuit diagram was (almost) the same. The interrupts that were used to change the LED's blinking speed is the same method that was used in the 03_altering_periodicity file. While working on the fsr--> LED Color tutorial, my code originally would not compile. I had copied and pasted the code from the tutorial page rather than downloading the associated files. In that code, the functions "setTarget" and "setColor" were referenced inside the "void loop ()" function, but they were not defined until after the loop. I placed the functions above the loop and ordered them so that each function was defined before it was referenced. Then, my code compiled successfully! The image below shows my compiling and flashing attempts along with the video of the working circuit. The led would change colors depending on the pressure applied to the force sensitive resistor, and they would gradually shift to meet the new color associated with each applied pressure.
<p align="center"><img width="40%" height="16" src="assets/white square.png">Click the image below to watch the video.</p>
<p align="center">
<img width="40%" alt="FSR to LED Color Terminal" src="assets/fsr-led-compile&flash.png">
<a href="http://www.youtube.com/watch?feature=player_embedded&v=TekFLnrGhPo" target="_blank">
 <img src="assets/fsr youtube thumbnail.png" alt="Watch the video" width=52% />
</a></p>

This week, I worked diligently to develop new skills. I was able to accomplish many activities and further my understanding of the Photon 2. Understanding how these physical components and software work together to accomplish each task will help me to create an ecosystem of my own. I still don't know what the project will be for this module, but if i had to speculate, I would imagine that we may be combining the use of the physical microcontroller, VS Code, an API, potentially copilot, and sensors to create some sort of responsive system. For example, with these tools, I could potentially have an LED light up every time someone enters the word "student" on their computer. I could make a game that lets someone's interaction with a distance sensor guide them through an obstacle course. I could possibly make some wheels turn using voice commands. There are many ways to combine the aformentioned skills to create a cohesive system of interworking parts.

---
## Week 4: Report 4 #
### 09/20/2024 - 09/26/2024

This week, I began to familiarize myself with interaction systems, which will enable the completion of TDF Project 2. Specifically, I studied how the AC Transit bus system works to connect me and my app to real-time bus locations. As shown in the diagram below, the user communicates with the app, which requests data from a server via an API. The data in the server is updated from a computer system on each bus. The computer system relies on location data that it recieves from the bus's GPS, and the GPS calculates its location with time delays and triangulation based on radio signals that is recieves from satellites.

<p align="center"><img width="95%" alt="AC Transit Ecosystem Diagram" src="assets/AC Transit Ecosystem Diagram.png"></p>

Understanding how different systems interact with one another to create a larger ecosystem allows will enable me to use the same principles for a project of my own. 

---
## Week 3: Report 3 #
### 09/13/2024 - 09/19/2024

This week, I completed my computational design project. Watch the video below for more details!

<p align="center"> Click the image below to watch the video.
<a href="http://www.youtube.com/watch?feature=player_embedded&v=ySvgrYaIrDs" target="_blank">
 <img src="assets/ComputationalDesignThumbnail.png" alt="Watch the video" width=95% />
</a></p>

While completing this project, I used Grasshopper, Rhino, a Cura Ultimaker Slicer, and a Prusa Mk4 printer. I decided to integrate a new cellphone stand design into the system provided by TJ that I had analyzed last week. I challenged myself to create an organic shape, and I customized the system's parameters to meet my phone specifications. The biggest challenge I faced was learning how to incorporate the graph mapper into my system, which took several tries and tutorial videos before it worked properly. I ultimately decided upon using a sine function to adjust the radii of the polygons that made up my cellphone base. I was able to manipulate different parameters until I was satisfied with the form, and I used the phone's boundary representation to create the cutout that would allow for my phone to sit properly in the base.

We were also able to hear from a guest speaker this week, who explained many other applications of computational design from modeling seed-planting mechanisms to creating oragami. Computational design offers a vast array of possibilities, which can help to increase accessibility, sustainability, inclusivity, and so much more. By augmenting human capabilities and allowing us to see how things will work before actually having to build them, this process allows for efficiency and iteration. We can also build models by taking in measurements and physical behaviors and using them to extrapolate more outcomes. Grasshopper is just one of many computational design tools, and I imagine that AI will also capitalize on the principles to further advance technological solutions.

---
## Week 2: Report 2 #
### 09/06/2024 - 09/12/2024

This week, I began to familiarize myself with Rhino and Grasshopper. I began by watching basic Rhino videos, and I reorganized my workspace to better suit my preferences. For example, I changed the layout of the view ports, making the perspective view port largest because I manipulate this view most often. Both the basic layout and my custom layout are shown below. The basic layout has four view ports of equal size, and a dark grey background. I changed the background to a lighter grey for aesthetic preferences along with rearranging the viewports.

<p align="center"><img width="45%" alt="Standard Rhino Setup" src="assets/rhino base setup.png">
<img width="50%" alt="Custom Rhino Setup" src="assets/rhino custom setup.png"></p>

I also began to explore grasshopper by analyzing the example phone stand file provided to the TDF class. I looked at the file and manipulated different input bars to see how each contributed to the stand that was displayed in Rhino. I also began to diagram my understanding of the file components. The example file looks like this.

<p align="center"><img width="95%" alt="Grasshopper Example File" src="assets/Grasshopper Example Screenshot.png"></p>

I began my diagram with a basic overview of the main sections of the file as shown below.

<p align="center"><img width="70%" alt="Overview Diagram" src="assets/Grasshopper Example Overview.png"></p>

From there, I went into more detail analyzing each part. I began with the fundamentals (purple) section, where the origin, planes, and prominent rectangular prism void were created. I then moved on to the creation of the cellphone stand (blue) before moving on to the creation of the cellphone itself (yellow). Each diagram is shown below.

<p align="center"><img width="40%" alt="Fundamentals Diagram" src="assets/Grasshopper Example Purple Breakdown.png"></p>
<p align="center"><img width="100%" alt="Cellphone Stand Creation Diagram" src="assets/Grasshopper Example Blue Breakdown.png"></p>
<p align="center"><img width="70%" alt="Cellphone Creation Diagram" src="assets/Grasshopper Example Yellow Breakdown.png"></p>

While analyzing the cellphone creation section, I noticed the use of a cluster. I did some research on how they worked, and learned that they operate like a function, allowing someone to condense a file that would otherwise be significantly larger. The much larger file containing the details of this cluster are shown in the screenshot below.

<p align="center"><img width="95%" alt="Cellphone Cluster Details" src="assets/Grasshopper Example Cell Phone Cluster Screenshot.png"></p>

Following the outputs of this cell phone cluster were options for toggling on/off different aspects of the cellphone display. There were also color swatch inputs, so I took the opportunity to turn the cellphone pink.

<p align="center"><img width="47.5%" alt="Before The Pink" src="assets/rhino setup screenshot.png">
<img width="47.5%" alt="After The Pink" src="assets/pink phone screenshot.png"></p>

After evaluating the example files and beginning to understand the software, I decided to create a structure using Grasshopper. I used basic components to create a box with adjustable inputs that has a cylindrical cutout in the center.

<p align="center"><img width="95%" alt="1st Grasshopper Creation" src="assets/first try grasshopper.png"></p>

This week, I pushed myself to understand new software, and I began to feel more comfortable with computational design. By diagramming the provideded example, I was able to conceptualize and analyze how different components worked together to create the intended structure. This understanding will allow me to create a computational design of my own, and I will be able to add inputs that allow for adjustments to be made. As I think about what could be accomplished with grasshopper, many things come to mind. Already, I have seen how this tool can be used to adjust parameters to accommodate different cellphone sizes and to change an object to adjust to different environmental conditions. The same can be true for other applications requiring customization such as casts, retainers, chairs, glasses, writing utensils, and more.


---
## Week 1: Report 1 #
### 08/30/2024 - 09/05/2024

This week, I designed a name plate for my desk! I used a laser cutter to fabricate the design after I created it in Adobe Illustrator. My goal was to become more familiar with the laser cutting equipment and associated software, which I did successfully. The completed name plate is shown here:

<p align="center"><img width="95%" alt="Completed Name Plate" src="assets/completed name plate.png"></p>

While the name plate turned out well, I found ways to expidite the process in the future. For example, I learned new short cuts for panning and zooming in Adobe Illustrator. Holding the spacebar while clicking with the mouse or touch pad allows for panning, while holding alt and scrolling with the mouse or touch pad allows for zooming in and out. While using the laser cutter, I noticed that the process was slower than anticipated. The total run time was 55 minutes and 43 seconds. However, I realized at least one way to reduce the time. There was a white square background behind the "B" in the name plate. As the laser cutter etched the large "B" the laser would travel nearly an inch past the actual etching points to what looked like the edges of the background box. This wasted time with unnecessary travel and could be fixed by removing the bounding box for future projects.

<p align="center"><img width="36%" alt="Completed Name Plate" src="assets/run time image.png">
<img width="59%" alt="Completed Name Plate" src="assets/laser cutter image.png"></p>

When deciding what to make, I wanted to use cutting, etching, and rastering operations to become familar with each process. I also chose to use both images and text in my illustrator file to learn how to properly convert each format to the proper format required by the laser cutters. I was able to find a template for a name plate <a href="https://www.instructables.com/Laser-Cut-Desk-Nameplate/">HERE</a>, which I subsequently customized. The example was made with acrylic, but I used wood for my project. When assembling it, it was difficult to fit the pieces together, but I was eventually able to struggle the wood into the slots.

<p align="center"><img width="60.85%" alt="Completed Name Plate" src="assets/name plate parts.png">  
<img width="34.15%" alt="Completed Name Plate" src="assets/name plate assembly.png"></p>

I also noticed this poster in the laser cutting room, which I may use in the future to test different joining methods and tolerances.

<p align="center"><img width="75%" alt="Completed Name Plate" src="assets/joints photo.png"></p>

---
