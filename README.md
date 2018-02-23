# Reliable top-left light convention starts with Early Renaissance:  An extensive approach comprising 10k artworks

Data and analysis for the __"Reliable top-left light convention starts with Early Renaissance:  An extensive approach comprising 10k artworks"__ manuscript.

## Analysis
The complete analysis, including all figures and statistical comparisons, can be found in Jupyter notebooks.

## Data

### Individual results files 
#### Files 
01KSC94w.csv, 02SEF89m.csv, 03SSK93m.csv, 04IKB95w.csv, 05SKL94w.csv, 06MMN92m.csv, 07HHA96w.csv.

If the cells starting with `SessionID` are empty, this means that the painting was never presented to that specific participant. 

#### CSV-format
* `medium`: painting medium, as described in the metadata at Wikimedia
* `painter`: painter, as described in the metadata at Wikimedia
* `title`: painting title, as described in the metadata at Wikimedia
* `url`: url to the online version of the painting
* `year`: year information, as described in the metadata at Wikimedia
* `local_filename`: filename of the local copy, serves as a unique painting ID
* `year_unambiguous`: disambiguated year in strictly numerical format. B.C. dates are negative.
* `Observer`: participant ID, matches the name of the file
* `SessionID`: session timestamp when the painting was evaluated
* `TrialTimestamp`: trial timestamp. Due to a programming mistake this column is missing for participants _01KSC94w_, _02SEF89m_, and _03SSK93m_.
* `FlippedLR`: whether the painting was left-right mirrored for the presentation
* `Confidence`: confidence about the estime, `0` confidence means no estimate was possible
* `Estimates`: a Python expression (list of dictionaries) with a complete history of estimates, if several attempts were made. The last dictionary in the list is the final estimate. Each dictionary has `'Start'` and `'End'` entiries that correspond to the star and the end points of the estimate. They contain a three element tuple: (`<x on-screen coordinate in pixels>`, `<y on-screen coordinate in pixels>`, `<time of the mouse click relative to the trial onset>`).
* `Duration`: a total trial duration from the trial onset till the confidence report or a "cannot estimate" report.
* `Painting CenterXY`: center of the painting on the screen in pixels, used to convert estimates from absolute on-screen coordinates to the relative ones.
* `Painting size`: size of the painting in pixels. Used to convert estimates from absolute on-screen coordinates to the relative ones.

### results_combined.csv
A single file containing all trial rows (_i.e._, excluding paintings which were not presented) from the individual participants files. Save csv-format as individual files.

### results_with_estimates.csv
Same as `results_combined.csv` but the explicit information about the _final_ estimate. If no estimate was possible (_i.e._, `Confidence` is zero), new columns are empty.
* `dx`: horizontal difference between end and start points of an estimate in pixels.
* `true_dx`: same as `dx` but the sign is flipped for left-right mirrored paintings
* `dy`: vertical difference between end and start points of an estimate in pixels.
* `angle`: estimate's direction in radians, computed from `dx` and `dy`
* `true_angle`: estimates true (corrected for mirrored paintings) direction in radians, computed from `true_dx` and `dy`
* `angle_deg`: same as `angle` but in degrees
* `true_angle_deg`: same as `true_angle` but in degrees

### paintings with estimates.csv
Contains average estimated direction of the light in the painting (corrected for mirrored paintings). Only for paintings __with__ an estimate.
* `local_filename`: local filename. Effectively, a painting ID.
* `year`: disambiguated year, identical to `year_unambiguous` in the results files.
* `estimate`: a mean direction in radians, effectivelly `mean(true_angle)`.
* `esimate.side`: -1 for left, 1 for right. Effectivelly, `sign(estimate)`.
* `confidence`: average confidence in estimates. Effectivelly, `mean(Confidence)`.

### PaintingsWithCountryInfo-EN.csv
Country of origin information about the inidividual paintings, extracted from the metadata as Wikimedia.
* `imgname`: unique painting ID, does not match `local_filename`
* `title`: painting title, as described in the metadata at Wikimedia
* `painter`: painter, as described in the metadata at Wikimedia
* `year`: year information, as described in the metadata at Wikimedia
* `medium`: painting medium, as described in the metadata at Wikimedia
* `image-URL`: url to the online version of the painting
* `page-URL`: url to the page with the metadata about the painting
* `OriginCountry`: extracted country of origin


## License
All data (and associated content) is licensed under the [CC-By Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/). All code is licensed
under the [MIT License](http://www.opensource.org/licenses/mit-license.php).