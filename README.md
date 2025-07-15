# RNAscopeQuantMouseBladder

RNAscope quantification macros code in ImageJ explanation. HAA edited 7.15.25

Step 1 — Select input images
•	When the macro runs, pop-up dialogs prompt you to select your DAPI, GREEN, CYAN, and MAGENTA channel images (one file each).
Step 2 — Preprocess each channel
•	For each channel:
•	Open the image and rename it to Channel_Original.
•	Convert to RGB Color mode → rename to Channel_RGB.
•	Convert to 16-bit → rename to Channel_16bit. (Preserves dynamic range)
•	Convert to 8-bit → rename to Channel_8bit.
•	This standardizes bit-depth for thresholding.
•	For DAPI only: duplicate the 8-bit version as DAPI_Main first.
•	Threshold the image:
o	DAPI: 80–255
o	Green: 60–255
o	Cyan: 60–255
o	Magenta: 145–255, with background subtraction (Subtract Background... rolling=25) before thresholding. (Background subtraction used for probe of interest due to high autofluorescence in bladder tissue)
•	Apply LUT to make threshold visible.
•	Duplicate the thresholded result as Channel_Main for merging later.
Step 3 — Merge channels and create overlays
•	All channels overlay: Merge DAPI (c3), Green (c2), Cyan (c5), Magenta (c6). Save as Overlay_All_Channels in RGB.
•	DAPI + Green overlay: Merge DAPI (c3) + Green (c2). Save as Overlay_DAPI_Green.
•	DAPI + Magenta overlay: Merge DAPI (c3) + Magenta (c6). Save as Overlay_DAPI_Magenta.
•	DAPI + Cyan overlay: Merge DAPI (c3) + Cyan (c5). Save as Overlay_DAPI_Cyan.
•	DAPI Main Grayscale: Convert DAPI_Main to RGB for consistent output.
Step 4 — Analyze particles for Magenta channel
•	Select Magenta_Main.
•	Run Analyze Particles:
•	Size: 2-25 pixels²
•	Circularity: 0–1
•	Show: Overlay
•	Display results, summarize, include overlay.
•	Convert Magenta_Main to a mask → rename to Magenta_Mask.
•	Run Analyze Particles again on the mask:
•	Same parameters but with Overlay Masks to show numbered labels.
•	Set overlay options: white outline, no fill, draw labels.
•	Flatten the labeled mask → rename Magenta_Mask_Flattened → convert to RGB.

