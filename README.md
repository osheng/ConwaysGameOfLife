<!--
*** To avoid retyping too much info. Do a search and replace for the following:
*** osheng, theGameOfLife, , email
-->



<!-- PROJECT LOGO -->
<br />
<p align="center">


  <h3 align="center">theGameOfLife</h3>

  <p align="center">
    This project is a verilog implementation of Conway's Game of Life.
    <br />
    <a href="https://github.com/osheng/ConwaysGameOfLife"><strong>Explore the repo »</strong></a>

  </p>
</p>



<!-- TABLE OF CONTENTS -->
## Table of Contents

* [About the Project](#about-the-project)
  <!--* [Built With](#built-with)-->
* [Getting Started](#getting-started)
  * [Prerequisites](#prerequisites)
  * [Setup](#installation)
* [Usage](#usage)
* [Roadmap](#roadmap)
* [Contributing](#contributing)
* [Contact](#contact)
* [Acknowledgements](#acknowledgements)
* [Where are the Verilog files?](#verilog-files)



<!-- ABOUT THE PROJECT -->
## About The Project
The Game of Life is a simulation on a grid where each cell has one of two states (populated or unpopulated) which all change based on the following rules.


###### The Rules
For a space that is 'populated':
* Each cell with one or no neighbors dies, as if by solitude.
* Each cell with four or more neighbors dies, as if by overpopulation.
* Each cell with two or three neighbors survives.

For a space that is 'empty' or 'unpopulated':
* Each cell with three neighbors becomes populated.


A user can do any of the following
* Load a predetermined state or saved states onto the grid
* Create their own with the mouse input
* Manually step through the simulation
* Automatically play the simulation
* Save states

These rules were copied from [here](https://bitstorm.org/gameoflife/).

###### Web Version
A web version of this project is available [here](https://bitstorm.org/gameoflife/).

###### More Info
More information about Conrad's Game of Life can be found on [Wikipdia](https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life).


<!--### Built With

* []()
* []()
* []() -->



<!-- GETTING STARTED -->
## Getting Started


### Prerequisites

Using this project requires the following.
* [Quartus 18+](http://fpgasoftware.intel.com/?edition=lite)
* a [DE1-SoC board](https://www.terasic.com.tw/cgi-bin/page/archive.pl?Language=English&No=836)
* a monitor with VGA input
* a Windows computer
* a PS2 mouse

<!--It's probable that this project can be used to program other FPGAs with little to no modification, but the authors of this project don't know which.-->


### Setup

1. Clone the theGameOfLife
```sh
git clone https://github.com/osheng/ConwaysGameOfLife.git
```
2. Create a new project named tGoL (the top-level module) in Quartus in the directory where you cloned theGameOfLife.
3. Import pin assignments from DE1_SoC.qsf
4. Compile the project. Note before compilation, you may want to change the localparams in tGoL.v
5. Use the programmer to program the FPGA. This is the only step that requires you use a Windows computer.

<!-- USAGE EXAMPLES -->
## Usage

* SW[9] toggles the clock on so the simulation automatically steps through each state. It is recommended to turn this off when toggling cells with the mouse, saving states, or loading states.
* SW[8] toggles the mouse on. Hold down right click, then left click to toggle a cell. Loading saved states will not work when mouse is on.
* SW[7] is not currently used.
* SW[6:5] select how fast the clock is. 00 is the fastest. 11 is the slowest.
* SW[4] toggles the cell and background colours.
* SW[3:0] selects which segment of memory to save to or load from. Note segments 0-3 and 15 cannot be overwritten in the 5x5 board or in the 40x28 board. Segment 4 also can't be overwritten in the 5x5 board.
* KEY[3] is the active low synchronous reset. Note this will not affect saved states.
* KEY[2] is the load key. Holding this down and pressing KEY[0] once will cause a state to be loaded to the board. Loading states will not work when mouse (SW[8]) is on.
* KEY[1] saves the current state to the selected segment of memory.
* KEY[0] steps the simulation forward by one state, when SW[9] is off.

Note: if the clock (SW[9]) is on and the mouse (SW[8]) is on, holding down right click will cause the selected cell to toggle with each clock pulse.


<!-- ROADMAP -->
## Roadmap
* tGoL.v --- TOP LEVEL MODULE (#TOPLEVELMODULE) for the whole project. This connects all the logic to the physical inputs and outputs.
* Board.v --- This is where all the cells live.
* Cell.v --- This is the top level module for cells.
* Adder.v --- This is the organelle in each cell which counts the output signals of adjacent cells.
* Decoder.v --- This is the organelle in each cell which takes the output from Adder and sends a signal to CellOut to say what the cell should do in the next state.
* CellOut.v --- This is the organelle in each cell which prepares the cell for its next update, whether that's a clock step or a new value being loaded in.
* VGADecoder.v --- This is the top level module for operating the VGA output.
* VGADecoderControl.v --- This is the control path for the VGADecoder.
* VGADecoderDatapath.v --- This is the datapath for the VGADecoder.
* RateDivider.v --- This provides a slower version of the 50MHz clock for playing the simulation at reasonable speeds.
* RateDividerComponent.v --- This helps modularize having different clock speeds come out of RateDivider.v
* HexDecoder.v --- This is used to decode the output to the seven segment displays.
* StateCounter.v --- This keeps track of how many states have passed since the last time we loaded in a state.
* Mouse.v --- This the top level module for the PS2 mouse inputs and outputs.
* SaveManager.v --- This is the top level module for the save and load board state functionality.
* SaveEncoder.v --- This modules determines what information to save in SaveManager to properly store the current board state in a way that it can be reloaded.
* SafetyMux*.v --- LPM_MUXs from Quartus' internal library to guard against random behaviour.
* ram16x*.v --- Quartus generated ram modules for saving board states.



<!-- CONTRIBUTING -->
## Contributing

This project is not actively maintained.




<!-- CONTACT -->
## Contact



Project Link: [https://github.com/osheng/theGameOfLife](https://github.com/osheng/theGameOfLife)



<!-- ACKNOWLEDGEMENTS -->
## Acknowledgements

* README format based off of [this template](https://github.com/othneildrew/Best-README-Template/blob/master/BLANK_README.md).
* HexDecode.v, DE1_SoC.qsf, black.mif, and the files in PS2MouseKeyboard, and the files in vga_adapter were provided by the instructors of CSC258 at UofT. SafetyMux*.v and ram16x*.v were generated by Quartus.

## Verilog files
This project has formed the basis for a paper on how using an FPGA to run cellular automata simulations can be faster even than using high end GPUs or CPUs with optimized algorithms. The paper has been submitted for publication. One of the co-authors has requested that we not publicly share the code at this time.





<!-- MARKDOWN LINKS & IMAGES -->
[license-shield]: https://img.shields.io/github/license/othneildrew/Best-README-Template.svg?style=flat-square
[license-url]: https://github.com/othneildrew/Best-README-Template/blob/master/LICENSE.txt
