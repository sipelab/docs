---
relatives:
  - "[[Dhyana 400BSI V2]]"
software:
  - "[[MicroManager]]"
  - "[[Python/Napari]]"
  - "[[pymmcore-plus]]"
  - "[[PsychoPy]]"
---
This camera is used to capture pupil dynamics during visual stimuli presented via [[PsychoPy]] on a [[Vis Stim Screen]] to collect videos of pupil diameter changes analyzed using [[DeepLabCut]]. 

The camera uses Thorlab's [Windows SDK](https://www.thorlabs.com/software_pages/ViewSoftwarePage.cfm?Code=ThorCam#) and drivers to interface with [[MicroManager]] to enable camera control through Python via [[pymmcore-plus]]
