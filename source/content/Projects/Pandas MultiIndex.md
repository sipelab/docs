### **Summary Table of Access Patterns**

| **GLOB_PATTERN Key**               | **Tuple (Before Padding)**   | **Column Key (After Padding)**  | **Access Example**                    |
| ---------------------------------- | ---------------------------- | ------------------------------- | ------------------------------------- |
| meso.ome.tiff                      | (`raw`, `meso`, `tiff`)      | (`raw`, `meso`, `tiff`)         | `df[("raw", "meso", "tiff")]`         |
| meso.ome.tiff_frame_metadata.json  | (`raw`, `meso`, `metadata`)  | (`raw`, `meso`, `metadata`)     | `df[("raw", "meso", "metadata")]`     |
| pupil.ome.tiff                     | (`raw`, `pupil`, `tiff`)     | (`raw`, `pupil`, `tiff`)        | `df[("raw", "pupil", "tiff")]`        |
| pupil.ome.tiff_frame_metadata.json | (`raw`, `pupil`, `metadata`) | (`raw`, `pupil`, `metadata`)    | `df[("raw", "pupil", "metadata")]`    |
| encoder-data.csv                   | (`raw`, `encoder`)           | (`raw`, `encoder`, "")          | `df[("raw", "encoder", "")]`          |
| *.psydat                           | (`raw`, `psydat`)            | (`raw`, `psydat`, "")           | `df[("raw", "psydat", "")]`           |
| _configuration.json                | (`raw`, `session_config`)    | (`raw`, `session_config`, "")   | `df[("raw", "session_config", "")]`   |
| full.pickle                        | (`processed`, `dlc_pupil`)   | (`processed`, `dlc_pupil`, "")  | `df[("processed", "dlc_pupil", "")]`  |
| meso-mean-trace.csv                | (`processed`, `meso_trace`)  | (`processed`, `meso_trace`, "") | `df[("processed", "meso_trace", "")]` |
