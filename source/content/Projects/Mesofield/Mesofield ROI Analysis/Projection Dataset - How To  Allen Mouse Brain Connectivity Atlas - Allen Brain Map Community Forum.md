---
title: "Projection Dataset - How To / Allen Mouse Brain Connectivity Atlas - Allen Brain Map Community Forum"
source: "https://community.brain-map.org/t/projection-dataset/2939"
author:
  - "[[Allen Brain Map Community Forum]]"
published: 2024-12-13
created: 2025-02-16
description: "Hi All, Thank you for this fantastic resource. Its really excellent and will save countless amounts of time, effort and funding. I recently discovered the ability to overlay the ISI imaging sessions in the “Cortical Ma&hellip;"
tags:
  - "clippings"
---
- [Searching](https://community.brain-map.org/t/projection-dataset/2939#searching-1)
- [Source Search](https://community.brain-map.org/t/projection-dataset/2939#source-search-2)
- [Target Search](https://community.brain-map.org/t/projection-dataset/2939#target-search-3)
- [Spatial Search](https://community.brain-map.org/t/projection-dataset/2939#spatial-search-4)
- [Using the Multiplanar Viewer to Search](https://community.brain-map.org/t/projection-dataset/2939#using-the-multiplanar-viewer-to-search-5)
- [Experiment Summary View](https://community.brain-map.org/t/projection-dataset/2939#experiment-summary-view-6)
- [Section Images Viewer](https://community.brain-map.org/t/projection-dataset/2939#section-images-viewer-7)
- [Projection Density Image Viewer](https://community.brain-map.org/t/projection-dataset/2939#projection-density-image-viewer-8)
- [Correlative Search](https://community.brain-map.org/t/projection-dataset/2939#Correlative-Search-9)
- [Cortical Map Viewer](https://community.brain-map.org/t/projection-dataset/2939#Cortical-Map-Viewer-10)
- [Viewing Projection Experiments](https://community.brain-map.org/t/projection-dataset/2939#viewing-projection-experiments-11)
- [Experimental Detail Page](https://community.brain-map.org/t/projection-dataset/2939#experimental-detail-page-14)
- [Experiment Image Viewer](https://community.brain-map.org/t/projection-dataset/2939#experiment-image-viewer-15)
- [Using the Section Images Viewer](https://community.brain-map.org/t/projection-dataset/2939#using-the-section-images-viewer-16)
- [Composite Projection Viewer](https://community.brain-map.org/t/projection-dataset/2939#composite-projection-viewer-20)
- [Composite View](https://community.brain-map.org/t/projection-dataset/2939#composite-view-21)
- [Contact Sheet Viewer](https://community.brain-map.org/t/projection-dataset/2939#contact-sheet-viewer-23)
- [High Resolution Image Viewer](https://community.brain-map.org/t/projection-dataset/2939#high-resolution-image-viewer-1)

## Searching

The Adult Mouse Connectivity Atlas comprises a searchable image database of axonal projections labeled by viral (rAAV) tracers and visualized using serial two-photon tomography.

Search this dataset using:

1. **Source Search** which allows searching by injection site (Filter source Structure(s)) and filtering by mouse line, tracer type and the presence of Intrinsic Signal Images  
![Search](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/7/74a79373500d37fd7b2b02e03ab253688557d4f0.png)
2. **Target Search** a “virtual retrograde” search that finds experiments based both on injection site and projection through a structure of interest  

[![TargetSearch](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/optimized/2X/6/6d2ff08d09258748ff7f8e9614ae1b5e8f9a980d_2_690x121.jpeg)](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/6/6d2ff08d09258748ff7f8e9614ae1b5e8f9a980d.jpeg "TargetSearch")
3. **Spatial Search** a spatial search allows the user to choose either a target signal or injection site based on selecting a voxel through which signal passes  

[![SpatialSearch](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/d/d07a45ec5e7a15a0d5701526f3464169d46e7521.png)](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/d/d07a45ec5e7a15a0d5701526f3464169d46e7521.png "SpatialSearch")

There are example searches in the *Browse Data* subject box on the landing page to demonstrate the various ways in which relevant data can be found. You can also browse experiments from the *3-D search result visualization*. Hovering your mouse over the dots (colored according to the [Reference Atlas](https://community.brain-map.org/t/adult-mouse-brain-reference-atlas/2768)) NEED LINK HERE will indicate the primary injection structure of that particular experiment.  

[![Visualization](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/optimized/2X/2/2f9d05f92a1e47a3f6d7f5d32d4e25d4c03ad0d3_2_690x369.png)](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/2/2f9d05f92a1e47a3f6d7f5d32d4e25d4c03ad0d3.png "Visualization")

Please see the Informatics Data Processing whitepaper available in the [Documentation](https://community.brain-map.org/t/documentation-mouse-connectivity-atlas/2940) tab for more information on the informatics processing performed in this study.

## Source Search

The default view is all experiments throughout the brain (indicated by “grey” and “retina”). To filter your search by injection site, select a structure(s) from the structure ontology that opens when you click in the “Filter Source Structure(s)” text box.

[![SourceSearch](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/optimized/2X/b/ba73ad0cc6e8f54451110e0a015e0e9da0c52b63_2_578x500.png)](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/b/ba73ad0cc6e8f54451110e0a015e0e9da0c52b63.png "SourceSearch")

From the Source Search, you also have the option to filter by mouse line or by tracer type. To filter by mouse line, click in the “Filter Mouse Line” text box and select from Wild Type, Cre line or Ai75(RCL-nt) options, or start typing in the text box to search tags from the various Cre-dependent mouse lines. The Ai75 (RCL-nt) option is a reporter strain that we used to target neurons within certain regions. When filtering using the “Filter Tracer Type” text box, you will have the option to choose between EGFP (axonal EGFP) experiments, SypEGFP (synaptophysin-tagged, synaptic EGFP) labeled experiments, or Target EFGP experiments. For more information on this targeting strategy, please see the Overview whitepaper in [Documentation](https://community.brain-map.org/t/documentation-mouse-connectivity-atlas/2940).

Although every effort was made to limit the injection site of the viral tracer to a single brain structure, it was often the case that cells in neighboring structures were also infected. We refer to these as “secondary injection structures” and include them in the results list as they may also contain interesting scientific information. To view these experiments as well, uncheck the “Primary Structure Only” box.

As we precisely target the higher visual areas in this data set, experiments utilized Intrinsic Signal Imaging for both guiding injections into the visual cortex, as well as to inform the interpretation of projection pathways. To view experiments that include these data, check the [Intrinsic Signal Images](http://ihelp.corp.alleninstitute.org/display/mouseconnectivity/Projection#Projection-ExperimentsincludingIntrinsicSignalImaging\(ISI\)) box.

As you select filtering parameters, notice that the number of experiments in the 3-D search result visualization decreases to show only the number of experiments that fit your search criteria.

Below the 3-D search result visualization, a list will automatically load with all the experiments that fit your filtering criteria.

This list includes:

| Column | Description |
| --- | --- |
| Checkbox | Select experiment(s) to view in the context of the reference datasets |
| Injection Structure | Abbreviations and color of primary injection structure (and secondary structures where applicable) |
| Mouse Line | Name of the mouse line used |
| Tracer | Tracer used in this experiment (EGFP, SypEGFP or Target EGFP) |
| Injection Volume | The volume of the injection site in cubic mm |

Clicking on the column headings will sort the list of experiments by that column, clicking twice on a single column will reverse the sort order. Once you have found a relevant group of experiments, you can save or bookmark these search results using the “Permalink” function.

![Permalink](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/a/a8911a99596afbaa8b73274396dbbd9e61e4b9a0.jpeg)  
Several experiments can be selected to view side-by-side and/or in the context of our [reference data](http://ihelp.corp.alleninstitute.org/display/mouseconnectivity/Reference+Data) by checking the boxes next to the experiments. Once you have selected the experiments you want to view, click the “View Selections” button. Those experiments will be available in your cart to view in the **Experiment Image Viewer** until you clear your cache or click the “Clear Selections” button.  
![ExpSelection](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/a/a39d1975403b16170ef06229637ee13dc4e9b1e4.png)  
Once you have narrowed your search and want to delve deeper into an individual experiment, open the **Experiment Summary View** by clicking on a circle in the 3-D search result visualization or an experiment in the list.

## Target Search

This search has all the same functional capabilities as **Source Search** with the added ability to filter your search by limiting the results to experiments where the projection signal passes through a given structure(s).

[![TargetSearchFull](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/8/85bc025823f9c7acd1a1190c3fb12576b93c9f6a.png)](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/8/85bc025823f9c7acd1a1190c3fb12576b93c9f6a.png "TargetSearchFull")

By default, when you click the “Target Search” radio button, the “Target Structure(s)” search box will open. After selecting one or more structures, selecting a hemisphere, or changing the minimum target volume (defaulted to 0.01 cubic mm), the 3-D search result visualization will automatically update with experiments that fit your filtering criteria. The list of experiments under the 3-D search result visualization includes the following information:

| Column | Description |
| --- | --- |
| Checkbox | Select experiment(s) to view in the context of the reference datasets |
| Injection Structure | Name of primary and secondary injection structure(s) including color of the structure according to the reference atlas |
| Mouse Line | Name of the mouse line used in this experiment |
| Injection Volume | The volume of the injection site in cubic mm |
| Target Volume | The volume of signal in the target structure in cubic mm |

Experiments are sorted by the target volume, but can be resorted by clicking on a column header. Once you have found a relevant group of experiments, you can save or bookmark these search results using the “Permalink” function.  
![Permalink](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/a/a8911a99596afbaa8b73274396dbbd9e61e4b9a0.jpeg)

Several experiments can be selected to view side-by-side and/or in the context of our [reference data](http://ihelp.corp.alleninstitute.org/display/mouseconnectivity/Reference+Data) by checking the boxes next to the experiments. Once you have selected the experiments you want to view, click the “View Selections” button. Those experiments will be available in your cart to view in the **Experiment Image Viewe** until you clear your cache or click the “Clear Selections” button.  
![ExpSelection](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/a/a39d1975403b16170ef06229637ee13dc4e9b1e4.png)

Once you have narrowed your search and want to delve deeper into an individual experiment, open the **Experiment Summary View** by clicking on a circle in the 3-D search result visualization or an experiment in the list.

Notice that experiments in the retina can be highlighted by hovering over the eye in the lower left-hand corner of the 3-D visualization or can be selected by clicking on one of the spheres indicating the entry point into the brain.  
![Retina](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/b/bdeebdd14c9c7b6086eeb4d4f8e503730b55b681.png)

## Spatial Search

[![SpatialSearch](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/d/d07a45ec5e7a15a0d5701526f3464169d46e7521.png)](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/d/d07a45ec5e7a15a0d5701526f3464169d46e7521.png "SpatialSearch")

Clicking the “Spatial Search” radio button allows you to do a voxel-based “virtual retrograde” search, or search for injection sites in close proximity to a selected voxel. The default view is pointed to a voxel in the ventral posterolateral nucleus of the thalamus, as indicated by the cross hairs in the **multiplanar viewer**. The 3-D search result visualization depicts all the injection sites with projection signal through the chosen structure. The approximate injection site is depicted with a sphere and the approximate pathway is traced with a line the same color as the injection site.

[![SpatialSearchsmaller](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/optimized/2X/0/0d942869c7a9a25f64979e3aa6ba70e422e7d80a_2_690x381.jpeg)](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/0/0d942869c7a9a25f64979e3aa6ba70e422e7d80a.jpeg "SpatialSearchsmaller")

Selecting the “Find Injection Sites” filter will bring up a threshold bar that will allow you to search for injection sites within a specified distance from your cross-hair location.  

[![InjSites](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/optimized/2X/a/ab1d825c5880f892205ecd725bc2eac402eb2a8e_2_690x387.jpeg)](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/a/ab1d825c5880f892205ecd725bc2eac402eb2a8e.jpeg "InjSites")

Click and drag the cross hairs in the **multiplanar viewer** to select a voxel in a particular structure. Once you have chosen a structure, you can further **filter** your search by selecting a mouse line and/or filtering by primary injection structure. The resulting list of experiments will include:

| Column | Description |
| --- | --- |
| Checkbox | Select experiment(s) to view in the context of the reference datasets |
| Injection Structure | Name and color of primary injection structure, and secondary injection structures (where applicable) |
| Mouse Line | Name of the mouse line used in this experiment |
| Injection Volume | The volume of the injection site in cubic mm |
| Target Density | The density of signal in the target structure as a ratio of pixels with signal over all pixels in the structure |

### Using the Multiplanar Viewer to Search

The voxel-based Spatial Search is carried out by using the multiplanar viewer. This viewer illustrates the Allen Mouse Common Coordinate Framework (CCF) and incorporates structures drawn in 3 dimensions: see the Mouse CCF whitepaper in [Documentation](https://community.brain-map.org/t/documentation-mouse-connectivity-atlas/2940). Access to the horizontal view is via the drop-down menu in the sagittal view.

[![SSHorizontal](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/optimized/2X/3/3b32b400064d662fab3efffc903b9f9c88ddb74f_2_300x500.jpeg)](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/3/3b32b400064d662fab3efffc903b9f9c88ddb74f.jpeg "SSHorizontal")

## Experiment Summary View

Hovering your mouse over an experiment will highlight that injection site in the 3-D search result visualization. Rotating the image in either the horizontal or vertical planes gives better access to view the selected experiments. To take a closer look at a particular experiment, click on that experiment, either in the list or on the 3-D search result visualization. Once an experiment has been chosen in this manner, a new panel of images and options will load on the right labeled by the Experiment ID number and the injection site structure. This view includes a **section images** viewer, a **projection density** image viewer, a transgenic characterization box, an injection summary for the rAAV virus injection and the targeting CAV injection summary (when appropriate) and a correlative search box. [Characterization](https://community.brain-map.org/t/transgenic-characterization/2941) of the transgenic lines used in this study has been carried out, and can be inspected from the link in the Transgenic Characterization box. If viewing an experiment from the Retinal Projectome, a whole mount view of the retina is available from a link in the Transgenic Line box. Experiments that show a similar signal pattern to the current experiment can be searched for using the **Correlative Search**.  

[![ExpSummaryView.PNG](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/optimized/2X/9/90dea43670bdd5909aa5a8788df4d54b1967548f_2_529x500.jpeg)](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/9/90dea43670bdd5909aa5a8788df4d54b1967548f.jpeg "ExpSummaryView.PNG")

Advanced search features are available from the icons in the toolbar of the experiment panel and include:

![CorticalMapIcon](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/1/183f0e329d462ee64524c03772a7daca82c7ef39.png): Open the experiment in a Cortical Map Viewer also where Intrinsic Signal Images (when available) will be displayed  
![SpatialSearchIcon](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/f/fefa577c7698fecd7f1db1197022c08c6d60c860.jpeg): Shortcut key to conduct a Spatial Search from the point indicated by the cross hairs  
![BEIcon](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/3/37da63fae6b8a24b25031141d343fc0b66013738.jpeg): Open the experiment in the 3-D Brain Explorer software  
![HRIV](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/0/0bfd27db086416bd59aa48e8599be6927f61b7df.jpeg): Open the experiment in a **High Resolution Image Viewer**  
![ExpDetIcon](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/7/7d80af7142688bb790584468092a5409dad14487.jpeg): Open quantification of the signal in the Experimental Detail page

### Section Images Viewer

![SegView](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/c/c637bcbec21fe19b921038c6e9ce7b97f9e6006f.jpeg)  
The section images viewer shows the 2-D fluorescence images in both the green (signal) channel and the red (autofluorescence) channel. Navigation (panning and zooming) through these images is achieved by using the on-screen navigation tools or using the **Keyboard Commands**.

This project utilizes extensive informatics processing and the informatics signal calculated by subtracting the background signal (segmentation images) can be viewed by clicking the ![Segmentation](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/d/d51079ba989f30a18db393e5388746dff9ab041c.jpeg) icon.

### Projection Density Image Viewer

This view shows an interactive 3-D thumbnail view of the experiment in what is referred to as the Maximum Intensity Projection (MIP) view. By default, a cross hair and sphere indicates the center of the injection site. Clicking on any other position in the MIP view will move the cross hair to the site selected both in the MIP view as well as in the 2-D view in the *section image view*. As selecting a point in a 3-D image can become problematic, you also have an option to view the intensity projection in 2-D from the drop-down menu that opens when you click on “MIP”. These views show the signal intensity against the two dimensional view of the Allen Mouse Common Coordinate Framework (CCF). For more information on the CCF, please see the whitepaper in the [Documentation](https://community.brain-map.org/t/documentation-mouse-connectivity-atlas/2940) tab.  

[![MultiPlanar](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/optimized/2X/5/599c8a7a7404bf4beeebfc3c5aff7261198afc5a_2_690x198.jpeg)](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/5/599c8a7a7404bf4beeebfc3c5aff7261198afc5a.jpeg "MultiPlanar")

The left (L) and right (R) sides of the brain are labeled in these views and navigation to the next section is achieved by clicking the < and > on-screen navigation buttons.

An example of the segmentation view is illustrated in the image to the right. For more information on the informatics processing in this project, please see the Informatics Data Processing whitepaper available from the [Documentation](https://community.brain-map.org/t/documentation-mouse-connectivity-atlas/2940) tab.

### Correlative Search

![CorrSearch](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/1/138d653945c050c9254aa1eb052b877f8fb59101.jpeg)  
Once you have found a relevant experiment, another useful search is for any other experiments that may show similar projection patterns. The correlative search allows you to look for similar patterns with an experiment of interest either by comparing brain wide (default), or by selecting fiber tracts or one of the other 12 major curated brain divisions available from the drop-down menu.

## Cortical Map Viewer

In order to enable the integration of information from different cortical depths, we constructed a curved cortical coordinate system. This coordinate system allows us to project structural features in the cortex, which are often oriented orthogonally to the surface, in a two dimensional plane that preserves structural integrity. When viewing projections in the Cortical Map, you are viewing the cortex along a “streamline” (see figure below and CCF whitepaper in [Documentation](https://community.brain-map.org/t/documentation-mouse-connectivity-atlas/2940).  
![CurvedCortex.PNG](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/6/68fe9fef0d0908679b91e4765379909e81d64dea.jpeg)  

[![CorticalMap.PNG](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/optimized/2X/4/40a52016fd2004a17af8c5315612e2ae584cfa1d_2_611x500.jpeg)](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/4/40a52016fd2004a17af8c5315612e2ae584cfa1d.jpeg "CorticalMap.PNG")

*When viewing this curved cortical coordinate system in two dimensions, structures such as the barrel fields in the somatosensory cortex and the primary visual cortex become visually distinct. While the curved cortical map nicely delineates the primary visual cortex, the associated visual areas are not so easily mapped. To further delineate these areas, Intrinsic Signal Imaging was performed during a visual stimulus to create sign maps for each individual brain.*

![SignMap](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/9/9905211a195ec0e072c1147056019150298b4071.jpeg)  
For more information on how the sign maps were generated, please see the Overview whitepaper in [Documentation](https://community.brain-map.org/t/documentation-mouse-connectivity-atlas/2940). The March 2016 data release was the first to include experiments that used sign maps to both target infection to specific visual areas as well as interpret projection from other brain regions to the visual areas.

![VisualAreas](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/1/164ff4eab55d9c915559bbf307ab3fa141cf48b5.png)

### Viewing Projection Experiments
#### Experiments without Intrinsic Signal Imaging (ISI)

When viewing an experiment of interest, you can visualize that experiment in the cortical map by clicking on the cortical map icon.  

[![example.PNG](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/optimized/2X/e/e074ac61c0b43269adddbe7801be724d9ea881bd_2_228x500.jpeg)](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/e/e074ac61c0b43269adddbe7801be724d9ea881bd.jpeg "example.PNG")

  

[![CortMapProjection.PNG](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/optimized/2X/c/c297444a11b8adad17368534375cee6b06e2917b_2_690x408.jpeg)](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/c/c297444a11b8adad17368534375cee6b06e2917b.jpeg "CortMapProjection.PNG")

Note: only the projection signal in the cortex is visible in the Cortical Map viewer.

*The cross-hairs on the Cortical Map indicate the location of the 2-D image from the experiment to the right. Navigation to other locations in the experiment is from either the on-screen navigation icons, or by double-clicking on the Cortical Map itself. Once a location has been chosen, the experimental ID, primary injection site, mouse line, position (in microns) and the location mapped to the [reference atlas](https://community.brain-map.org/c/how-to/reference-atlases/23) will show up in the left-hand corner of the screen. Clicking on the experimental ID link will take you to the Experimental Detail Page. Only the Projection Density and Structures checkboxes will be available for experiments without ISI.*

#### Experiments including Intrinsic Signal Imaging (ISI)

To see experiments that include ISI, make sure to check the “Intrinsic Signal Images” box in your initial search.  
Once an experiment with ISI has been selected, a radio button will appear which allows overlay of the projection and ISI views.

[![Overlay.PNG](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/optimized/2X/f/fcf452cad9aa85932f344da4a046fbe5e1ea888b_2_431x500.jpeg)](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/f/fcf452cad9aa85932f344da4a046fbe5e1ea888b.jpeg "Overlay.PNG")

*The cross-hairs on the Cortical Map indicate the location of the 2-D image from the experiment to the right (not shown). Navigation to other locations in the experiment is from either the on-screen navigation icons, or by double-clicking on the Cortical Map itself. Once a location has been chosen, the experimental ID, primary injection site, mouse line, position (in microns) and the location mapped to the [reference atlas](https://community.brain-map.org/c/how-to/reference-atlases/23) will show up in the left-hand corner of the screen. Clicking on the experimental ID link will take you to the Experimental Detail Page.*

## Experimental Detail Page

The experimental detail page illustrates the projection experiment in an informatically quantified fashion. This page contains the Injection Summary(ies), a Projection Density Image Viewer, a Section Images Viewer, and a histogram quantifying the signal in each region, displayed either by Projection Volume or Projection Density.  

[![ExpDetail](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/optimized/2X/f/fe0ed51d51fce8fb11ec72b8f914c43c67032fe3_2_603x500.png)](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/f/fe0ed51d51fce8fb11ec72b8f914c43c67032fe3.png "ExpDetail")

1. **Injection Summary:** This section includes a link to the Cortical Map Viewer from the icon in the top right-hand corner and lists the experiment ID, primary and secondary injection structure(s), the coordinates of the injection, the mouse strain, tracer type and the calculated injection summary (%) for the rAAV injection and the CAV injection (where appropriate). If the experiment was targeted stereotaxically, the coordinates are from a registration point (typically Bregma) in the anterior/posterior, dorsal/ventral, medial/lateral orientations and the angle of injection (AP, ML, DV, <). If the experiment was targeted using ISI, the coordinates will read “ISI(0, 0, DV, <)” indicating the depth and angle of injection (see Overview whitepaper in Documentation). If the experiment shown is from a transgenic line, you will also have a description of the infected cells and a link to the [Transgenic Characterization](https://community.brain-map.org/t/transgenic-characterization/2941) of that line.
2. **Projection Density Image Viewer:** This viewer offers a rotating preview of the projection signal in 3 dimensions. Click the “View in 3D” link to view the experiment in the [Brain Explorer](https://community.brain-map.org/t/brain-explorer-3d-viewer/2986r) software.
3. **Section Images Viewer** The Section Images viewer allows you to browse the experiment in 2-D. You can scroll through thumbnails of each section, zooming in or out and panning through areas of interest.  
![ProjVolDen](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/2/2cdf50876f2977d99cdab77b984cb3923b7718c8.jpeg)
4. **Histogram:** This section illustrates the quantified signal in each structure either by projection volume (mm3) or by projection density (fraction of area occupied by signal compared to the whole structure). Toggle the two representations of the data using the drop down menu at the top of the histogram. The selected structure ontology can be expanded or collapsed and the number of structures shown can be changed using the threshold slider bar at the top of the histogram. When you click on a structure in the histogram, you will be taken to that area of the brain in the 3-D and 2-D image viewers. A red cross-hair pinpoints the center of that structure in each of the image viewers.

Data from this page can be downloaded as XML.

## Experiment Image Viewer

To view several experiments in a single window, check the boxes next to experiments of interest from the various search methods. Once you have selected “View Selections” a window will open with all your checked experiments. The experiment image view displays images for each selected experiment in a Section Images viewer. This view makes it easy to compare experiments with each other and with the associated reference atlas, and with the Reference Data.

![ref-atlas-choose](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/7/7b7e2b88221fe59cb167e58f814ba0128aa9d5f9.jpeg)

Multiple image series can be opened on the same page to enable side-by-side comparisons. Arrange the experiments by dragging an image viewer by the title bar and dropping into a new location. Add a reference atlas by selecting one from the “Atlases” drop-down menu in the upper-right hand corner of the window (see screenshot).

If you are viewing more than one experiment, open the configuration options to change the number of columns displayed in the window. The configuration options are accessible by clicking on the button with a “gear” icon to the right of the “Atlases” menu.

The injection site, section number and experiment ID are displayed in the title bar. Experiments using transgenic mice will also report the name of the transgenic line. Icons in the toolbar allow for you to take actions on the current image.

To view an overlay of each of the selected experiments in the Experiment Image Viewer, click on the Composite Projection Viewer in the title bar.

### Using the Section Images Viewer

The Section Images Viewer is a powerful tool to navigate and view the images in an experiment. The main part of the viewer is an interactive window where an image can be repositioned by dragging with a mouse. Use the scroll wheel, on-screen navigation buttons or the keyboard to zoom in or out.

Thumbnails for the entire image series are displayed across the bottom of the viewer in section order. Click a thumbnail to select it for viewing, or use the keyboard to navigate through the set. The current selection is outlined in black.  
![ZAP](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/2/26a590e66d9413c46ab39abd4f0a39984e2b039f.jpeg)

#### Scale Bar

Drag the scale bar with your mouse to the desired location. Click the scale bar text with your mouse to toggle between horizontal and vertical scale bars.

#### Using the Section Images Viewer Toolbar

Use the toolbar to take actions on the current image. Toolbar controls include:  
![ZAP_menu](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/6/66eed977c5ea6a1c50a2bc4b12a9104143dc44e3.jpeg): Select between raw data and projection segmentation images  
![image_adj](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/0/056cdbd6dda3089d24f085df6dc001aa47516735.jpeg): Adjust image controls  
![image_adj](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/0/056cdbd6dda3089d24f085df6dc001aa47516735.jpeg): View all images in this experiment in a Contact Sheet Viewer  
![sync](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/c/c26c2485ef2696c6cf3fb800b11ea01650ee086e.jpeg): Synchronize all other section image viewers on the page that support synchronization to the currently selected image  
![close](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/f/ff8fb30ea360609c34ea7cc8fe0491de69c09cfb.jpeg)" Close the Section Images viewer

#### Keyboard Commands

Use the keyboard to navigate through the image series and synchronize the viewers on the page. Keyboard commands include:

| Key | Function |
| --- | --- |
| A | Zoom in |
| Z | Zoom out |
| F | Step forward through the thumbnail images keeping the same location and scale |
| D | Step backward through the thumbnail images keeping the same location and scale |
| S | Sync all viewers on the page to the zoom level and location of the active viewer |
| + | Zoom in. Please note that some keyboards may require the \[Shift\] key be held down while pressing the \[+\] key |
| \- | Zoom out |

You can also use the arrow keys to pan the current image.

## Composite Projection Viewer

The Composite Projection Viewer allows you to see several projection experiments overlaid on the reference brain. This view allows you to sync experimental images with the reference atlas and other reference data.  

[![CompositeView](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/optimized/2X/9/901c90d70bf3deb9d04042383c3c7c8d586845de_2_554x500.jpeg)](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/9/901c90d70bf3deb9d04042383c3c7c8d586845de.jpeg "CompositeView")

The elements of this viewer include:

1. Toggle between the individual image viewers and the composite viewer
2. Add the coronal or sagittal reference atlas (will display below the Composite View) or change the number of columns (from the “gear”)
3. The Composite View. Clicking the “+” in the top left-hand corner will open up images of each experiment
4. Display reference data such as the annotated reference atlas or histochemical stains that was already in your viewing cart

### Composite View

![dots](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/6/62b92a326fb5d951a8116f1ddd41d77a8709df23.png)  
The composite view illustrates each selected experiment in an arbitrary color as circles based on the signal density in that voxel. Navigate the image viewer using the onscreen navigation tools or the options in the toolbar.  
![sites](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/c/ceb7335f4bb33e85435772359ce538492404a140.png)

#### Composite View Toolbar

![orientation](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/4/47427d64324b915bba9dba27e799beaca2e2a39b.png): Choose your orientation - coronal, sagittal or horizontal  
![scale](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/c/c5d651a265d5dd29e9f216672aea6afd1bed5a97.png): Change the size of the circle (0-3 Ergs)  
![slice](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/f/ffbb2d16478a761b5403e11d4d43adff798bc54d.png): Move through the sections with the slider bar (microns)  
![sync](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/9/9328579acd4a72e13d7928df6c8716fcdb0a20e0.png): Sync composite image to the reference data  
![brainexplorer](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/c/c27f6c430e87d7c58fbabe01533a0ed962d9a912.png): See selected experiments in the Brain Explorer 3-D Viewer

### Contact Sheet Viewer

The contact sheet viewer shows serial sections of the selected experiment. Background fluorescence in the red channel illustrates basic anatomy and structures of the brain, and the injection site and projections are shown in the green channel.  

[![ContactSheet](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/optimized/2X/3/3b5dc0197c9c93a08c6f1df630a5cd9e388eda06_2_690x389.jpeg)](https://canada1.discourse-cdn.com/flex027/uploads/brainobservatory/original/2X/3/3b5dc0197c9c93a08c6f1df630a5cd9e388eda06.jpeg "ContactSheet")

Double-clicking on individual images on the contact sheet will launch a High Resolution Image Viewer.