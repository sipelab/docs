---
website: https://www.psychopy.org/index.html
relatives:
  - "[[MicroManager]]"
  - "[[XYZ Stage Control]]"
docs:
  - "[[Resources/PsychoPy/Psychopy autorun]]"
  - https://www.psychopy.org/documentation.html
controls:
  - "[[Vis Stim Screen]]"
---

[Download](https://www.psychopy.org/download.html)

[How to Build a PsychoPy Experiment](https://workshops.psychopy.org/3days/day1/buildingBetter.html)


Need a timestamp variable:
```python
import time
timestamp = time.strftime("%Y-%m-%d_%H-%M-%S")
```


Output filename:
![[Pasted image 20250128130411.png]]
```python
u'data/%s/sub-%s/ses-%s/beh/sub-%s_ses-%s_%s' % (expInfo['Subject ID'], expInfo['Session ID'], expInfo['Subject ID'], expInfo['Session ID'], timestamp)
```
![[Pasted image 20250128130527.png]]
# How to parameterize a PsychoPy script from the builder


> [!warning] Keep in Mind
> This tutorial is intended for generating a PsychoPy experiment as a script that will be run as a subprocess using the Python `subprocess` module or the PyQt process module. These modules will launch the script using command line arguments, which provide parameters defining the experiment type. We will discuss how to run the PsychoPy script at the end.


## 1. Build a custom code block for system input and output:

- You need to place this in the **[Before experiment*]*** tab so that the script 'asks' for arguments once it is launched and before the experiment loop initiates
	![[PsychoPy_io-routine.png]]
	
```python
#======== Custom Codeblock jgronemeyer =====================================#
#add system argument functionality
#Get command line arguments passed if present
sysarg_protocol_id = None
sysarg_subject_id = None
sysarg_session_id = None
sysarg_save_dir = None
sysarg_nTrials = None # changed data.TrialHandler2 object value nReps value to call this variable
if len(sys.argv) > 1:
    sysarg_protocol_id = sys.argv[1]  # get the first argument from command line
    sysarg_subject_id = sys.argv[2]  # get the second argument from command line
    sysarg_session_id = sys.argv[3]  # get the third argument from command line
    sysarg_save_dir = sys.argv[4]  # get the fourth argument from command line
    nTrials = sys.argv[5] # get the fifth argument from the command line
    #encoder = sys.argv[6] # TODO: accept encoder parameters
#==============================================================================#
```

> [!NOTE] Tip
> I suggest adding commented delimiters ("#------#") to make finding codeblocks in the raw Python script more intuitive 



## 2. Setup a trial loop and set the `Num. repeats` variable to `nTrials`. 

- Notice that `nTrials` is an expected argument in the system input argument list. This allows the input at the start of the script to define the number of trials for the experiment.
- Make sure you have inserted a loop into the experiment Flow

	![[PsychoPy_trial-loop.png]]
	![[PsychoPy_nTrials.png]]



## 3. We need to save the custom data 

- Create a custom code block and call it `save_custom_format`. In this example, I am using the BIDS standard for saving behavioral data. Add this to the `End experiment*` tab of the Custom Code block
	![[PsychoPy_save-bids.png]]
	
```python
#==== Custom Codeblock jgronemeyer =====================================#
# Sipelab standard BIDS protocol file naming for 
#   future batch analysis and data wrangling
protocol_id = expInfo['Protocol ID']
subject_id = expInfo['Subject ID']
session_id = expInfo['Session ID']
timestamp = datetime.now().strftime('%Y%m%d_%H%M%S') # get current timestamp (BIDS)

# Extend PsychoPy's `_thisDir` with the custom directory path `save_to`
save_to = f'data/{protocol_id}/sub-{subject_id}/ses-{session_id}/beh'
new_directory = os.path.join(_thisDir, save_to)

# Create the path if it does not exist
if not os.path.exists(new_directory):
    os.makedirs(new_directory)

#Generate the filename for saving encoder_data
encoder_filename = os.path.join(new_directory, f"sub-{subject_id}_ses-{session_id}_{timestamp}_wheeldf.csv")

if encoder_data is not None:
    encoder_data.to_csv(encoder_filename, index=False)
else:
    print("No encoder data in `encorder_data`")
#==============================================================================#
```

> [!question] Reading Encoder Data
> You'll notice the logic for saving `encoder_data` to a csv. See the tutorial for implementing a threaded serial reader during a PsychoPy experiment


## 4. I suggest creating a Routine to hold these two Custom Code blocks:

- Routine: `InputOutput`
	- Codeblock1: `get_input_argument`
	- Codeblock2: `save_bids_format`


## 5. Insert the `InputOutput` Routine at the beginning of the experiment Flow in the PsychoPy Builder

![[PsychoPy_InputOutput-routine.png]]

## 7. Disable the `Show info dialog` option. 

- This is the normally how PsychoPy asks for user inputs about experiment parameters. However, we need to disable it in order to run the script with command line arguments
![[PsychoPy_disable-dialog.png]]

## 8. Compile the experiment as a Python script, and save it to your desktop 


## 9. Create a batch script for testing the experiment.

- This will pass some arguments, and launch the experiment using the PsychoPy python environment. You will need to have installed PsychoPy from the website.  Open up a Notepad or plaintext editor and paste something like:

```batch
:: Set variables which are going to be needed for the experiment.
:: Read: set /parameter [variable] equal to [userinputprompt]
set /p protocol=protocol_id:
set /p subject=subject_id:
set /p session=session_id:
set /p savedir=save_dir:
set /p trials=nTrials:


:: Note to pay attention to the order, as we call them in the experiment by the order in which they are put in here.
:: Read: python -m script.py %arg% %arg% %arg% %arg% %arg% where each %arg% is a [variable]
"C:\Program Files\PsychoPy\python.exe" D:\path\to\your\psychopy\script\Gratings_vis.py %protocol% %subject% %session% %savedir% %trials%
```

> [!warning] Keep in Mind
> The ordering of variables *must* match between the script and the initial input. This is because the PyschoPy script will iterate through the list of given parameters one-by-one. Fancier methods of accomplishing this (such as storing all arguments in a Python dict object with keys named for each value), but the current solution is elegant enough--and it **works**.

## 8. Save your batch script as something like `launch_psychopy_with_args.bat` 

- Now, you can double click this file to launch the command. For it to work, it must have the correct number of parameters, a valid path to the Psychopy python installation, and a valid path to the Psychopy script itself.


## 9. Put the `psychopy_script.py` in a folder with the `launch_psychopy_with_arg.bat` file. 

- Launch the batch script, enter argument manually, and ensure the experiment runs. Look for a `\Data` file within this folder containing output from the PsychoPy experiment run.