# DESCRIPTION

Perform text detection in a variety of languages with computer webcam using Google Tesseract OCR and OpenCV. 
This script achieves a real-time OCR effect by incorporating multi-threading.

Requires Tesseract to be installed. Tesseract is free and easy to install on Mac, Windows, and Linux.

# DETAILS

An OpenCV video stream runs in a dedicated thread, so it's always reading live frames from the webcam and storing the most recent in memory as a class attribute. The video display can access these frames and show them in real-time. Meanwhile, pytesseract OCR has its own dedicated class, running in a dedicated thread, and it simply grabs the most recent frame from the video stream class, processes it, and returns the detected text when it is finished processing. Without any form of multi-threading or multiprocessing, a frame display loop would have to wait for the OCR text detection to complete analysis before showing a new frame, creating a large bottleneck for most implementations. Multi-threading improves the processes significantly by allowing the video stream to run in real-time while the OCR works in the background. Boxes and detected text are dispalyed as they are updated by the OCR thread. One limitation is that the OCR is still limited in processing speed and will not return a bounding box and detected text for every frame from the video stream, but for ordinary applications where the camera has several seconds to analyze stable text this lag is managable. 

This script is easily modifiable to work with other camera sources, image types, and image processing methods since it is an implementation of the OpenCV video stream.

# USE

This a command-line script. The only required argument is a full path to the Tesseract executable from the Tesseract install (see DEPENDENCIES below for more info) 

`python Main.py -t '<full_path_to_your_tesseract_executable>'


# Image Capture and Quit

While running an OCR stream, push "c" to capture the current frame and save as a .jpeg to the working directory. A capture will also print the current detected text to the command line:

# DEPENDENCIES

This script requires:
- a Tesseract install
- the python wrapper for Teseract (pytesseract)
- OpenCV for python (CV2)
- Numpy

# PROGRAM CONTENTS

Main.py
- Command-line argparser and call to the OCR stream

OCR.py
- All classes and functions for multi-threaded text detection and webcam display

Linguist.py
- A few functions for handling the language codes and converting them to full language names (reads from Tesseract_Langs.txt)

Tesseract_Langs.txt
- Text file for every supported language code and the language's full name

README.md

requirements.txt

