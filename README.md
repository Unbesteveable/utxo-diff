<!-- ABOUT THE PROJECT -->

## Project Overview

This project advances the utxo-live project by visualizing the difference between two states of the Bitcoin blockchain. A new feature in Bitcoin Core 0.20 allows users to dump the state of the blockchain (the UTXO set) using the command `dumptxoutset`. While the previous project utxo-live visualized the indivdiual UTXO sets, this project visualizes the differences (the coins spent) between the two states of the chain.
 
<br>

<img src="https://utxo.live/utxo_diff_678336_to_680188.png" alt="Logo" >
<em>Figure description: The heatmap is a two dimensional histogram showing the output date (x-axis), BTC amount (y-axis), and number of unspent outputs (color map) in each histogram bin. The bin size of the histogram is 200 (yaxis) by 400 (xaxis). Zooming in to the image usually reveals more detail. A daily updating version of this image is running at <a href=https://utxo.live/changes/yesterday.php/>utxo.live</a>.</em>


## Privacy & Security

With the new `dumptxouset` command, the python script no longer requires an RPC password to access Core's databases. The script simply reads the dump files without interacting with Core at all. No private keys, passwords, xpubs, or wallet addresses are exchanged between Core and the python script.


<!-- Requirements -->
## Requirements
* Bitcoin Core version 0.20 or higher
* Python3 (comes standard on all operating systems)


## Instructions for experienced users
* Create a folder called `utxo-live` in a familiar location
* Dump the utxo set `bitcoin-cli dumptxoutset <path to utxo-live>/xxxxxx.dat` where xxxxxxx is the current block height (5 min)
   (Note: `bitcoin-cli` doesn't ship with Core on Mac OS, use Window->Console instead)
* Wait until a later block height, and repeat the step above using the larger block number
* Install two python dependencies `python3 -m pip install numpy matplotlib` 
* Download <a href='https://github.com/Unbesteveable/utxo-live/raw/main/utxo-live.py'>utxo-live.py<a> to your `utxo-live` folder and run it `python3 utxo-live.py` (20 min)

## Step by step instructions
1. Make sure Bitcoin Core (version 0.20 or higher) is running and synchronized.

2. Create a new folder called `utxo-live` in a familiar location on your machine (e.g. in your Documents folder).

3. Open a terminal window and display the current folder path. Do this by:

  * Windows: open a terminal (Start -> Command Prompt) and type: 
  ```sh
  echo %cd%
  ```
  
  * Mac/Linux: open a terminal (Mac: Applications -> Utilities -> Terminal) and type:
  ```sh
  pwd
  ```
  
4. Navigate to the `utxo-live` folder using the change directory `cd` command. For example if you're currently in `Users/Steve/` (or on Windows `C:\Users\Steve\`) and you've created the folder  `Steve/Documents/bitcoin-tools/utxo-live/` then type: 

  ```sh
  cd Document/bitcoin-tools/utxo-live/
  ```
  Note: Windows sometimes requires forward slashes `/` instead of back slashes `\`.
  
5. Again display the current folder (Step 3) and copy to your clipboard the full path to the `utxo-live` folder. We will be pasting this path into Bitcoin Core soon.

6. Leave the terminal window momentarily, and open the Bitcoin Core console window. (Alternatively for bitcoin-cli users, open another terminal window and type the console commands in the next steps as `bitcoin-cli` commands.)

<img src="https://miro.medium.com/max/1098/1*DEukIfd6csdA6bbl2K5sSg.jpeg" alt="Open Console Pic" >

7. Get the current block count by typing in the console window:

  ```sh
  getblockcount
  ```
  and hitting enter. The output will look like:

<img src="https://utxo.live/getblockcount.png">
 

8. Dump the current utxo set by typing in the console window:

```sh
  dumptxoutset <PATH to utxo-live>/<xxxxxx.dat>
  ```
  where `<PATH to utxo-live>` is copy-pasted from Step 5, and `<xxxxxx.dat>` is the block count. For example if the block count is 678505, the command (for my path) is:

```sh
  dumptxoutset /Users/Steve/Documents/bitcoin-tools/utxo-live/678505.dat
  ```
  If there are no error messages after hitting enter, then it's working. It will take 5-10 minutes. Look in your `utxo-live` folder and you should see the file being created as `xxxxxx.dat.incomplete`.

9. While the utxo file is dumping, download `utxo-live.py` and install two python dependencies. To do this:
 
 * Right click on <a href='https://github.com/Unbesteveable/utxo-live/raw/main/utxo-live.py'>utxo-live.py<a>, choose "Save Link As" and select the `utxo-live` folder.

 * In the terminal window (not the Bitcoin console), type the following command to install two python dependencies:
```sh
  python3 -m pip install numpy matplotlib
  ```

   Note: you might already have these installed, but running the command won't hurt anything.

10. If ten minutes have passed, check that the utxo dump is completed. Do this in two ways:

   * Check that the file no longer has `.incomplete` after `xxxxxx.dat` 
   * Check that the Bitcoin Core console displays the results of the dump as something like:

<img src="https://utxo.live/dump_output2.png">

11. If the dump file is finished and Step 9 is completed (<a href='https://github.com/Unbesteveable/utxo-live/raw/main/utxo-live.py'>utxo-live.py<a> is downloaded and python dependencies were installed), then run <a href='https://github.com/Unbesteveable/utxo-live/raw/main/utxo-live.py'>utxo-live.py<a> by typing in the terminal:

```sh
  python3 utxo-live.py
  ```

12. The program will take 20-30 minutes to complete and it will update you on the progress. If there are multiple xxxxxxx.dat files in the folder, it will ask you which one you'd like to process. When finished the image is stored in the folder as `utxo_heatmap_xxxxxx.png`.


## Acknowledgements

I'm indebted to three main projects for the code, understanding, and inspiration for this project. The python functions that parse and decode the utxo dump file were adapted from <a href='https://github.com/sr-gi/bitcoin_tools'>Bitcoin_Tools<a>. I learned how Core serializes utxos from <a href='https://github.com/in3rsha/bitcoin-utxo-dump'> Bitcoin-UTXO-Dump <a>. An inspiring project that visualizes changes in the UTXO set as a movie is <a href='https://github.com/martinus/BitcoinUtxoVisualizer'> BitcoinUtxoVisualizer <a>.
 
 
 
