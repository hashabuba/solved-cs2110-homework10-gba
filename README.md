Download Link: https://assignmentchef.com/product/solved-cs2110-homework10-gba
<br>
The goal of this assignment is to make an interactive C program (e.g. a game, an interactive storybook, an application of other sorts) that will run on the GBA emulator. Your program should include everything in the requirements and be written neatly and efficiently. Your code should be something different from lecture code, since in this homework you will be creating your own program, but keep the core setup with videoBuffer, MODE 3, waitForVBlank, etc.

Prototypes, #defines, and extern declarations should be put into header files such as logic.h, graphics.h, or gba.h. It is also optional for you to use other .c/.h files to organize your logic if you wish, just make sure you include them in submission and Makefile.

We want to make one point very clear: please do not rehash lecture code in your program. This means that you are not allowed to just slightly modify lecture code and to call it a day. If we open your program and we see several boxes flying in random directions, that will be a very bad sign, and you will not receive a very pleasant grade. Also, please do not make Pong. Everyone asks if they can make Pong, and it’s just a boring, low-effort product in general.

<h1><a name="_Toc10639"></a>2           Assignment Details</h1>

<strong>IMPORTANT! READ THIS SECTION VERY CAREFULLY.</strong>

<h2><a name="_Toc10640"></a>2.1         Resources</h2>

To help you structure your project, we have provided you with a number of files as a template. These files contain comments marked <strong>TA-TODO </strong>for things that need to be worked on. Some of these are things that you <strong>MUST </strong>have in your submission as explained in the requirements section below, such as waitForVBlank. Others are things that we have included to guide you to intelligently structure your project. As a result, before starting with your project, <strong>make sure you search in the entire directory for the string TA-TODO to find all the things we recommend that you do.</strong>

The structure we give you is as follows:

<ul>

 <li><em>c </em>contains the state machine behind the application that controls what screen you are in, waits for VBlank, and calls all other functions.</li>

 <li><em>c/h </em>contain the GBA macros and the low-level drawing functions, as well as a random number generator that you can use.</li>

 <li><em>c/h </em>contain prototypes for functions that you will write that will draw your app on the screen.</li>

 <li><em>c/h </em>contain structs and function prototypes for the logic layer behind your app. The idea here is that we keep the logic and graphics layers separate: the app, with all its relevant information, is entirely maintained as a struct while the graphics layer in <em>graphics </em>is responsible for representing this logical app on the screen.</li>

 <li><em>c </em>contains the font that the text-drawing functions use. You can swap this out with any font you want to use.</li>

 <li><em>images/ </em>is a good place to put the .c and .h files corresponding to images you want to use, produced by nin10kit.</li>

</ul>

Some ideas that we put in the structure that we recommend you implement are as follows:

A VBlank Counter: in <em>gba.c/h </em>we declare and initialize a vblankCounter variable that you will increment every time we wait for VBlank. Then you will be able to use this variable from inside your <em>processAppState </em>etc. functions to do something once every fixed number of frames, for example, move a snake every 10 frames by checking if <em>vblankCounter % 10 == 0</em>.

<ul>

 <li>Key Just Pressed macro: in <em>c/h </em>we give you a Key Just Pressed macro that you can use to determine if the key has been recently pressed, i.e. it wasn’t ‘down’ before but it is now. You need to implement this macro (it’s essentially this previous sentence, in C, using the <em>KEY </em><em>DOWN </em>macro). We keep track of the previous and current key inputs in <em>main.c </em>and pass those to <em>processAppState </em>for you to use this macro with.</li>

 <li>Current and Next AppState: in <em>c </em>we give you two structs in which we maintain the app state: currentAppState and nextAppState. The purpose of this is to enable the calculation of everything about the next state without having to wait for vblank, but then doing the drawing during VBlank. We need the previous state for exactly this reason: even after we have calculated the next state, we need to be able to access the previous state to be able to undraw (i.e. erase) the elements in the previous state that might have moved. In fact, you can use this setup to compare elements between the two states so that you only draw what has changed.</li>

</ul>

<strong>However, the structure that we give you is only a suggestion. You do NOT need to use any of the files we give you, in fact, you do NOT need to use anything we give you, as long as your code satisfies the requirements and the command </strong><em>make </em><strong>produces a .gba file. Feel free to manipulate the template we give you in absolutely any way you want</strong>.

<h2><a name="_Toc10641"></a>2.2         Content Requirements</h2>

<ul>

 <li>You must use 3 distinct images in your program, all drawn with DMA.

  <ul>

   <li>Two full screened images sized 240 x 160. One of these images should be the first screen displayed when first running your program.</li>

   <li>A third image which will be used during the course of your program. The width of this image may not be 240 and the height of this image may not be 160.</li>

   <li>Note: all images should be included in your submission</li>

  </ul></li>

 <li>You must be able to reset the program to the title screen AT ANY TIME using the select key</li>

 <li>Button input should visibly and clearly affect the flow of the program</li>

 <li>You must have 2-dimensional movement of at least one entity. One entity moving up/down and another moving left/right alone does not count.</li>

 <li>You should implement some form of object collision. For programs where application of this rule is more of a gray area (like Minesweeper), core functionality will take the place of this criteria, such as the numbers for Minesweeper tiles calculated correctly, accurate control, etc.</li>

 <li>You must implement waitForVBlank.</li>

 <li>Use text to show progression in your program.</li>

 <li>There must be no tearing in your program. Make your code as efficient as possible!</li>

</ul>

<h2><a name="_Toc10642"></a>2.3         Code Style Requirements</h2>

<ul>

 <li>Must be in Mode 3 unless you’re absolutely sure you want to try something else, without TA support.</li>

 <li>You must also implement a drawImage function with DMA.</li>

</ul>




Put your prototypes, struct declarations and typedefs in header files. Do not put functions in header files.

<ul>

 <li>You must use at least one struct.</li>

 <li>Include a readme.txt file with your submission that briefly explains the program and the controls.</li>

 <li>Do not include .c files into other files. Only .h files should be included and .h files should contain no functional code.</li>

</ul>

<strong>While full credit will be given for submissions that satisfy all the above requirements, extra credit for submissions that go above and beyond may be given at TA and instructor discretion.</strong>

<h2><a name="_Toc10643"></a>2.4         What to Make?</h2>

You may either create your own program the way you wish it to be as long as it covers the requirements, or you can make programs that have been made before with you own code. However, your assignment must be yours entirely and not based on anyone else’s code. This also means that you are not allowed to base your program off the code posted from lecture. Programs that are lecture code that have been slightly modified are subject to heavy penalties. Here are some previous programs that you can either create or use as inspiration:

<strong>Hint: It’s better to be creative and come up with something new than reuse these!</strong>

<strong>Galaga:</strong>

<ul>

 <li>Use text to show lives</li>

 <li>Game ends when all lives are lost. Level ends when all aliens are gone.</li>

 <li>Different types of aliens: there should be one type of alien that rushes towards the ship and attacks it</li>

 <li>Smooth movement (aliens and player) <strong>The World’s Hardest Game:</strong></li>

 <li>Smooth motion for enemies and player (no jumping around)</li>

 <li>Constriction to the boundaries of the level</li>

 <li>Enemies moving at different speeds and in different directions</li>

 <li>Sensible, repeating patterns of enemy motion</li>

 <li>Enemies and the Player represented by Structs <strong>Flyswatter:</strong></li>

 <li>Images of yellow jackets or flies moving smoothly across the screen</li>

 <li>Player controlled flyswatter or net to catch the flies</li>

 <li>Score counter to keep track of how many flies have been swatted</li>

 <li>Fullscreen image for title screen and game background</li>

 <li>Enemies and the Player represented by Structs</li>

</ul>

<strong>Interactive Storybook:</strong>

Recreate a story from a movie or a book using the GBA

<ul>

 <li>Use text to narrate what is currently happening in the scene</li>

 <li>Use the controls to advance to the next scene or control a character within the scene</li>

 <li>Satisfy the collision requirement by having a cursor etc. element whose position needs to be used to calculate where it’s pointing.</li>

 <li>Smooth movement (for any moving characters or objects)</li>

 <li>Start off with a full screen title image and end with a full screen credits image <strong>Data Visualization App:</strong></li>

 <li>Use the GBA to visualize a dataset that you can include in your code. Can be a 2d plot.</li>

 <li>Use text to draw the scale of the axes.</li>

 <li>Use a cursor and apply collision calculation to click and zoom on individual datapoints.</li>

 <li>Implement zooming etc. animations without tearing.</li>

</ul>

<h1><a name="_Toc10644"></a>3           Warnings</h1>

<ul>

 <li>Do not use floats or doubles in your code. Doing so will slow your code down greatly. The ARM7 processor the GBA uses does not have a Floating Point Unit which means floating point operations are slow and are done in software, not hardware. Anywhere you use floats, gcc has to insert assembly code to convert integers to that format. If you do need such things then you should look into fixed point math.</li>

 <li>Only call waitForVBlank once per iteration of your main loop</li>

 <li>Keep your code efficient. If an <em>O</em>(1) solution exists to an algorithm and you are using an <em>O</em>(<em>n</em><sup>2</sup>) algorithm then that’s bad (for larger values of n)! For example, <strong>do not pass large structs directly to functions </strong>but pass pointers instead so that only a single pointer needs to be copied onto the stack rather than the full struct.</li>

 <li>If you use more advanced GBA features like sprites or sound, making them work is your responsibility; we (the TAs) can not help you.</li>

</ul>

<h1><a name="_Toc10645"></a>4           Deliverables</h1>

Please run make submit and upload submission.tar.gz to Gradescope under the Homework 10 assignment.

This includes all .c and .h files needed for your program to compile. Do not submit any compiled files. You can use make clean to remove any compiled files. (make submit will do this automatically.) Gradescope will confirm that your Makefile produces a valid .gba file when make is run.

<strong>Download and test your submission to make sure you submitted the right files. </strong>The Gradescope tester just checks that you submitted compiling code — not that you submitted what you thought you did.

<h1><a name="_Toc10646"></a>5           GBA Coding Guidelines</h1>

<h2><a name="_Toc10647"></a>5.1         Installing Dependencies</h2>

There are some dependencies for running the tests.

If you are using Docker, re-run cs2110docker.sh to stop the old container, download updates to the image (which include these dependencies), and restart the container.

If you are using a VM, run

$ sudo apt update

$ sudo apt install gcc-arm-none-eabi cs2110-vbam-sdl mednafen cs2110-gba-linker-script nin10kit

Note that this requires Brandon “The Machine” Whitehead’s CS 2110 PPA, which you should’ve added earlier in the class for complx. If you didn’t (or this is a new VM or something), run the following and then run the two commands above again:

$ sudo add-apt-repository ppa:tricksterguy87/ppa-gt-cs2110

<h2><a name="_Toc10648"></a>5.2         Building and Running your Code</h2>

To build your code and run the GBA emulator, run

$ make emu

<h2><a name="_Toc10649"></a>5.3         Images</h2>

As a requirement, you must use at least 3 images in your program and you must draw them all. To use images on the GBA, you will first have to convert them into the suitable format. We recommend using a tool called nin10kit, which you installed with the command above.

You can read about nin10kit in the nin10kit documentation (there are pictures!):

<a href="https://github.com/TricksterGuy/nin10kit/raw/master/readme.pdf">https://github.com/TricksterGuy/nin10kit/raw/master/readme.pdf </a>nin10kit reads in, converts, and exports image files into C arrays in .c/.h files ready to be copied to the GBA video buffer by your implementation of drawImage! It also supports resizing images before they are exported.

You want to use Mode 3 since this assignment requires it, so to convert a picture of smelly festering garbage into GBA pixel format in garbage.c and garbage.h, resizing it to 50 horizontal by 37 vertical pixels, you would run nin10kit like

$ cd images/

$ nin10kit –mode=3 –resize=50×37 garbage garbage.png This creates a garbage.h file in images/ containing

extern const unsigned short garbage[1850];

#define GARBAGE_SIZE 3700

#define GARBAGE_LENGTH 1850

#define GARBAGE_WIDTH 50

#define GARBAGE_HEIGHT 37




which you can use in your program by saying #include “images/garbage.h”.

The images/garbage.c generated, which you should add to the Makefile under OFILES as images/garbage.o if you plan to use it, contains all of the pixel data in a huge array:

const unsigned short garbage[1850] =

{

0x7fff,0x7fff,0x7fff,0x7fff,0x7fff, // …

0x7fff,0x7fff,0x7fff,0x7fff,0x7fff, // … // …

0x7fff,0x7fff,0x7fff,0x7fff,0x7fff, // …

0x7fff,0x7fff,0x7fff,0x7fff,0x7fff, // …

};

We’ve included garbage.png, garbage.c, and garbage.h in images/ directory in the homework tarball so you can check them out yourself. To draw the garbage in your own game, you can pass the array, width, height to your drawImage like drawImage(10, 20, GARBAGE WIDTH, GARBAGE HEIGHT, garbage) (to draw at row 10 and column 20). The next section will cover drawImage in more detail.

<h2><a name="_Toc10650"></a>5.4         DMA / drawImage</h2>

In your program, you must use DMA to implement image drawing.

Drawing to the GBA screen follows the same guidelines as the graphics functions you had to implement for HW9. The GBA screen is represented with a short pointer declared as videoBuffer in the gba.h file. The pointer represents the first pixel in a 240 by 160 screen that has been flattened into a one dimensional array. Each pixel is a short and has a red, green, and blue portion just like the pixels in HW9. With a little modification (Hint: include the graphics and geometry header files and use videoBuffer as the screen buffer), you should be able to use the same code you implemented in HW9 to draw to the GBA screen. Note that those functions do not use DMA and thus are considerably slower than the ones you will implement for this assignment.

DMA stands for Direct Memory Access and may be used to make your rendering code run much faster. If you want to read up on DMA before it is covered in lecture, you may read these pages from Tonc. <a href="http://www.coranac.com/tonc/text/dma.htm">http://www.coranac.com/tonc/text/dma.htm</a> (Up until 14.3.2).

If you want to wait, then you can choose to implement drawImage without DMA and then when you learn DMA rewrite it using DMA. Your final answer for drawImage must use DMA.

You must not use DMA to do one pixel copies (Doing this defeats the purpose of DMA and is slower than just using setPixel!). Solutions that do this will receive no credit for that function. When drawing an image, you should know that DMA acts as a for loop, but it is done in hardware. You should call DMA for each row of the image and let DMA handle drawing all of the columns in that row of the image.

<strong>For drawing a fullscreen image, a single DMA call suffices. Why? Try implementing this in your code.</strong>

<h2><a name="_Toc10651"></a>5.5         GBA Controls</h2>

Here are the inputs from the GameBoy based on the keyboard we’ve configured for the recommended emulator mednafen (these are the same as the default controls for vbam, an alternate emulator):

<table width="147">

 <tbody>

  <tr>

   <td width="71">Gameboy</td>

   <td width="76">Keyboard</td>

  </tr>

  <tr>

   <td width="71">Start</td>

   <td width="76">Enter</td>

  </tr>

  <tr>

   <td width="71">Select</td>

   <td width="76">Backspace</td>

  </tr>

  <tr>

   <td width="71">A</td>

   <td width="76">Z</td>

  </tr>

  <tr>

   <td width="71">B</td>

   <td width="76">X</td>

  </tr>

  <tr>

   <td width="71">L</td>

   <td width="76">A</td>

  </tr>

  <tr>

   <td width="71">R</td>

   <td width="76">S</td>

  </tr>

 </tbody>

</table>

The directional arrows are mapped to the same directional arrows on the keyboard.

<h2><a name="_Toc10652"></a>5.6         C Coding Conventions</h2>

<ul>

 <li>Do not jam all your code into one function (i.e. the main function) • Do not include .c files into other files. Only .h files should be included.</li>

 <li>.h files should contain no functional code.</li>

 <li>Comment your code, and comment what each function does. The quality of your comments will be factored into your grade!</li>

</ul>