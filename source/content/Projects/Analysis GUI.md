
**Goal**: An analysis gui should be aware of files within a directory of specific file type and with specific filename-endings.

**Description**: A core component is to allow the exploration of data from an experimental session. A session usually produces two memory mapped ome tiff stacks and wheel encoder speed. The software should synchronize the data to a common time dimension, allowing users to scrub through all of the data at once, synchronously. 

This is accomplished by synchronizing the time metadata from several files
	`_encoder-data.csv`
	`_meso.ome.tiff_frame_metadata.json`
	`_thor.ome.tiff_frame_metadata.json`

The file hierarchy is standardized in BIDS format. Users should be able to select a folder where this file structure exists within:
- PsychoPy trial data and wheel encoder data are found in the /beh folder
	`data/protocol/subject/session/beh`
- The ome.tiff stacks are found in the /func folder
	`data/protocol/subject/session/func`
```wasm
data/
    protocol/
        subject/
            session/
                func/
                beh/
```
## Current example code
```python
def load_metadata(directory):
    frame_metadata_df = None
    pupil_frame_metadata_df = None

    # Parse the directory for files ending with '_frame_metadata.json' and 'pupil_frame_metadata.json'
    for file in os.listdir(directory):
        if file.endswith('meso_frame_metadata.jsonf'): 
            frame_metadata_path = os.path.join(directory, file)
            frame_metadata_df = load_frame_metadata(frame_metadata_path)
        elif file.endswith('pupil_frame_metadata.jsonf'):
            pupil_frame_metadata_path = os.path.join(directory, file)
            pupil_frame_metadata_df = load_frame_metadata(pupil_frame_metadata_path)

    return frame_metadata_df, pupil_frame_metadata_df
```

```python
def plot_encoder_csv(encoder_df, psychopy_df):
    speed = encoder_df.iloc[:, 2]
    time = encoder_df.iloc[:, 1]

    plt.plot(time, speed)
    plt.xlabel('Time')
    plt.ylabel('Speed')

    for idx, row in psychopy_df.iterrows():
        if pd.notna(row['stim_label']):
            start_time = row['Checkerboard.started']
            label = f"{row['stim_label']}_{row['direction']}"
            plt.axvline(x=start_time, linestyle='--', label=label)

    plt.title('Speed over Time')
    plt.legend()
    plt.show()
```

```python
        dh_md_df, th_md_df = data.load_metadata(self.config.bids_dir)
   data.plot_encoder_csv(data.load_wheel_data(self.config.bids_dir), data.load_psychopy_data(self.config.bids_dir))

```

Then, the file paths for the tiff stacks are standardized as:
	`_meso.ome`
	`_pupil.ome`

The result should be a gui that shows both the meso and pupil videos above the speed plot for a session. There should be a dropdown selection that parses json files in the parent directory above the BIDS directory; once a file is selected it should be displayed as a table for viewing. 

**File Search Summary**

| Data Type                               | Directory                   | Filename Pattern                      |
| --------------------------------------- | --------------------------- | ------------------------------------- |
| Wheel Encoder Data                      | `/beh`                      | `_encoder-data.csv`                   |
| [[PsychoPy]] Data                       | `/beh`                      | Psychopy CSV/JSON files               |
| [[Dhyana 400BSI V2\|Meso]] Metadata     | `/func`                     | `_meso.ome.tiff_frame_metadata.json`  |
| [[Thorlabs CS165 MU\|Pupil]] Metadata   | `/func`                     | `_pupil.ome.tiff_frame_metadata.json` |
| [[OME Data Model\|OME]] TIFF Stacks     | `/func`                     | `_meso.ome` and `_pupil.ome`          |
| Session-Level JSON files (for dropdown) | Parent directory above BIDS | `*.json`                              |
