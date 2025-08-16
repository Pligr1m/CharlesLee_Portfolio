# Optical Character Recognition
For my project, I built a system that combines OCR (Optical Character Recognition) with speech-to-text (STT) and text-to-speech (TTS) to read and interpret text from both images and live audio. One of the biggest challenges was optimizing the camera and preprocessing images to accurately capture and recognize as much text as possible. Completing the project taught me how to integrate multiple AI tools seamlessly, and it was incredibly rewarding to see the system both read text from a camera feed and speak it aloud in real time.


| **Engineer** | **School** | **Area of Interest** | **Grade** |
| ------------- |:-------------:| :-------------: |:-------------:|
| Charles L.  | Roslyn High school| Civil/ Environmental engineering| Rising Junior |





![Headstone Image](poop.jpeg)
 
# Final Milestone



<iframe width="1013" height="570" src="https://www.youtube.com/embed/168AbMPATOo" title="Charles L. Milestone 3" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>


- For my final milestone I was able to implement a new camera for clearer images/ more consistent image recognition and a speaker for text to speech reconition:

  I implemented text to speech by using pyttsx3 library which allows for text to be changed into speech from my ocr
 

### Challenges

- My biggest challenge at BSE was learning how to code and apply software, which set me back from adding the OLED or button to my project. I also faced issues with incompatible libraries, corrupted SD cards, and software compatibility with the Raspberry Pi’s operating system. Despite these setbacks, I completed the base of my project(Optical Character Recognition) and added extra componenets such as STT (speech-to-text) and TTS (text-to-speech) features.

### Learnings from Blue Stamp

- My journey at BSE was filled with valuable learning experiences, especially with Python. I learned how to use Python to control different aspects of my project, from running code on the Raspberry Pi to integrating software features like speech-to-text and text-to-speech. Through trial and error, I developed a stronger understanding of Python’s syntax, libraries, and problem-solving applications, which gave me the confidence to build and expand my project’s functionality.
 
### What I plan to do after BSE

- In the future after BSE, I hope to learn more about machine learning and its implementation in the real world and how it can help people. Looking forward, I am eager to deepen my understanding of machine learning by creating and training my own models. I want to explore how these models can be applied to solve problems that humans can't solve on their own and ultimately use them to make a positive difference in society. By learning more about the principles and applications of machine learning, I hope to develop tools and technologies that can help people and contribute to building a better future.

CODE
MILESTONE 3

UPDATED OCR


# Second Milestone
<iframe width="1013" height="570" src="https://www.youtube.com/embed/XhUOV3ATmAE" title="Charles L. Milestone 2" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

- For my second milestone I started to work on my speech to text recognition. I firstly began by installing vosk which is an offline speech recognition built using machine learning that allows you to convert spoken words into text. I also added additional features which allowed certain keywords to trigger and made it respond to certain words from speech. Lastly, I integrated the OCR with the camera so it was able to recognize text from pictures taken by my camera

### Challenges
- A problem I had was that the packages to download vosk became corrupted and the camera was not recognizing text in many images. I was able to fix the corrupted files and replace them. The problem I encountered for the camera wasn't as straight forward since I wasn't able to compeltely change the camera to take higher resolution pictures, I figured out that lighting affected the camera's ability to recognize text and started to use additional lighting while taking photos.

### Surprises
- Something that surprised me was how many resources there are online for coding and engineering. Whenever I run into an error, I can usually find someone who had the same issue and solved it. I like how open and helpful the engineering community is. These resources have helped me grow a lot as an engineer, letting me solve problems on my own by researching and putting in the time, without always relying on my mentor or teacher to help.

### Milestone #3 Plans
- For my final milestone I would like to implement a button that can take a picture with my camera, an oled screen that displays text, and finally implementing text to speech translation for my OCR

CODE
MILESTONE 2

STT CODE
```

import sounddevice as sd
import vosk
import queue
import json
import asyncio
from datetime import datetime
from googletrans import Translator

# Initialize Google Translator (sync API)
translator = Translator()

# Vosk Model path
MODEL_PATH = "/home/clee27/Documents/vosk-model-small-en-us-0.15"
model = vosk.Model(MODEL_PATH)
recognizer = vosk.KaldiRecognizer(model, 16000)

q = queue.Queue()

def callback(indata, frames, time, status):
    q.put(bytes(indata))

# Async wrapper around googletrans.translate() to make it non-blocking
async def translate_text(text, src='auto', dest='en'):
    result = await asyncio.to_thread(translator.translate, text, src=src, dest=dest)
    return result

async def translate_and_respond(text):
    print(f"Translating: {text}")

    # Translate to English
    result_en = await translate_text(text, dest='en')
    print(f"EN: {result_en.text}")

    # Translate to Japanese
    result_ko = await translate_text(text, dest='ko')
    print(f"KO: {result_ko.text}")


    # Translate Latin phrase
    result_la = await translate_text('veritas lux mea', src='la', dest='en')
    print(f"Latin: {result_la.text}")

async def main():
    loop = asyncio.get_running_loop()

    with sd.RawInputStream(samplerate=16000, blocksize=8000,
                           dtype='int16', channels=1, callback=callback):
        print("Say something...")

        while True:
            data = await loop.run_in_executor(None, q.get)

            if recognizer.AcceptWaveform(data):
                result = json.loads(recognizer.Result())
                recognized_text = result['text']
                print("You said:", recognized_text)

                # Keyword-based responses
                if "hello" in recognized_text:
                    print("Hi there! How can I help you?")
                elif "time" in recognized_text:
                    now = datetime.now().strftime("%H:%M")
                    print(f"The current time is {now}")
                elif "bye" in recognized_text or "exit" in recognized_text:
                    print("Goodbye!")
                    break  # Exit loop

                # Async translation for recognized text
                if recognized_text is not None or not recognized_text.isspace():
                   
                    await translate_and_respond(recognized_text)

            else:
                partial = json.loads(recognizer.PartialResult())
                print("Partial:", partial['partial'])

# Run the async main loop
asyncio.run(main())



```
This code listens to your microphone and changes what you say into text using the Vosk speech recognition library, and is able to react to certain keywords. It is also able to translate english to korean


OCR CODE
```
from picamera2 import Picamera2
import cv2
import pytesseract
import numpy as np
from pytesseract import Output
import time
import pyttsx3  # <-- Added for text-to-speech

# ========== Step 1: Initialize camera ==========
print(" Initializing camera...")
picam2 = Picamera2()
picam2.configure(picam2.create_preview_configuration(main={"format": "RGB888", "size": (1280, 720)}))
picam2.start()

time.sleep(2)  # Let the camera warm up

# Best frame tracking
best_char_count = 0
best_frame = None
best_processed_images = []
best_text = ""  # <-- store best recognized text

# Preprocessing functions
def get_grayscale(image):
    return cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

def thresholding(image):
    return cv2.threshold(image, 0, 255, cv2.THRESH_BINARY + cv2.THRESH_OTSU)[1]

def opening(image):
    kernel = np.ones((5, 5), np.uint8)
    return cv2.morphologyEx(image, cv2.MORPH_OPEN, kernel)

def canny(image):
    return cv2.Canny(image, 100, 200)

print(" Capturing frames for 10 seconds and finding the best OCR result...")

start_time = time.time()
while time.time() - start_time < 10:
    # Capture a frame
    frame = picam2.capture_array()
    img_source = cv2.fastNlMeansDenoisingColored(frame, None, 10, 10, 7, 21)

    # Processed image variations
    processed_images = [
        img_source,
        get_grayscale(img_source),
        thresholding(get_grayscale(img_source)),
        opening(get_grayscale(img_source)),
        canny(get_grayscale(img_source))
    ]

    # Count characters from all processed versions
    total_chars = 0
    combined_text = ""
    for img in processed_images:
        text = pytesseract.image_to_string(img)
        combined_text += text + " "
        total_chars += len(text.strip())

    # Update best result if this frame is better
    if total_chars > best_char_count:
        best_char_count = total_chars
        best_frame = frame.copy()
        best_processed_images = processed_images.copy()
        best_text = combined_text.strip()
        print(f" New best frame with {best_char_count} characters.")

print(" Capture complete. Saving best processed images...")

# Prepare thresholded image from best frame for consistent OCR detection
threshold_img = thresholding(get_grayscale(best_frame))

# Save best frame variations with bounding boxes from thresholded OCR
for i, img in enumerate(best_processed_images):
    output_img = img.copy()

    # Convert grayscale or canny images to color for drawing
    if len(output_img.shape) == 2:
        output_img = cv2.cvtColor(output_img, cv2.COLOR_GRAY2RGB)

    d = pytesseract.image_to_data(threshold_img, output_type=Output.DICT)
    n_boxes = len(d['text'])
    for j in range(n_boxes):
        if int(d['conf'][j]) > 60 and d['text'][j].strip():
            x, y, w, h = d['left'][j], d['top'][j], d['width'][j], d['height'][j]
            cv2.rectangle(output_img, (x, y), (x + w, y + h), (0, 255, 0), 2)
            cv2.putText(output_img, d['text'][j], (x, y - 10),
                        cv2.FONT_HERSHEY_SIMPLEX, 0.8, (0, 255, 0), 2)

    output_path = f'img{i}.jpg'
    cv2.imwrite(output_path, output_img)
    print(f" OCR result saved as {output_path}")

print(f" Best frame had {best_char_count} recognized characters.")
print(f" Best recognized text:\n{best_text}")



```
This program turns on the Pi camera and captures an image for 10 seconds afterwards, it tests different filters to make text easier to read. Lastly, it picks the picture with the most recognized text and saves the image.

# First Milestone


<iframe width="1013" height="570"
    src="https://www.youtube.com/embed/YlaM46ZHwUE"
    title="Charles L. Milestone 1"
    frameborder="0"
    allowfullscreen>
</iframe>


- The 2 main componenets of my project are the raspberry pi 4 and the camera that connects onto it. Aditionally, I used Visual Studio to create a virtual environment with the specific packages needed for my project, made a script called camera.py that sets up the Pi camera and takes a photo which is saved to the device. Also made a script for the program to process the images which I named example.py

- I learned why a virtual environemt was needed and how the terminal was used to connect to the raspberry pi without being physically connected.

- One challenge I faced was dealing with errors while installing the required packages. Even after reinstalling the Raspberry Pi OS, the system still failed to detect the camera as a connected device. I also ran into difficulties connecting Visual Studio to the Raspberry Pi. Since Python was relatively new to me, it slowed down my progress and set me back from my original plan for Milestone 1.
 
- I resolved the package errors by installing them outside the virtual environment, which stopped the recurring issues. I also fixed the connection problem between Visual Studio Code and the Raspberry Pi by making sure the Pi was connected to my local Wi-Fi network.
 
-I plan to integrate speech-to-text functionality into the project as well as a translation component to support multilingual input and output.


# Code
Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs.

example.py
```c++
import cv2
import pytesseract
import numpy as np
from pytesseract import Output
 
img_source = cv2.imread('coffee-ocr.jpg')
 
 
def get_grayscale(image):
    return cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
 
 
def thresholding(image):
    return cv2.threshold(image, 0, 255, cv2.THRESH_BINARY + cv2.THRESH_OTSU)[1]
 
 
def opening(image):
    kernel = np.ones((5, 5), np.uint8)
    return cv2.morphologyEx(image, cv2.MORPH_OPEN, kernel)
 
 
def canny(image):
    return cv2.Canny(image, 100, 200)
 
 
gray = get_grayscale(img_source)
thresh = thresholding(gray)
opening = opening(gray)
canny = canny(gray)
 
i=0
for img in [img_source, gray, thresh, opening, canny]:
    d = pytesseract.image_to_data(img, output_type=Output.DICT)
    n_boxes = len(d['text'])
 
    # back to RGB
    if len(img.shape) == 2:
        img = cv2.cvtColor(img, cv2.COLOR_GRAY2RGB)
 
    for i in range(n_boxes):
        if int(d['conf'][i]) > 60:
            (text, x, y, w, h) = (d['text'][i], d['left'][i], d['top'][i], d['width'][i], d['height'][i])
            # don't show empty text
            if text and text.strip() != "":
                img = cv2.rectangle(img, (x, y), (x + w, y + h), (0, 255, 0), 2)
                img = cv2.putText(img, text, (x, y - 10), cv2.FONT_HERSHEY_SIMPLEX, 1.2, (0, 255, 0), 3)
 
    cv2.imwrite(f'img{i}.jpg', img)
    i+=1
    cv2.waitKey(0)
```
-This script processes an image using various different techniques in order to detect and highlight readable text, then saves the results. It makes use of image processing and OCR tools to extract and display the text visually. The script simplifies the entire text detection process.

camera.py
```c++
from picamera2 import Picamera2
import cv2

# Initialize PiCam
picam2 = Picamera2()
picam2.configure(picam2.create_preview_configuration(main={"format": "RGB888", "size": (640, 480)}))
picam2.start()

# Capture one frame
frame = picam2.capture_array()

# Save the image to disk
cv2.imwrite("image.jpg", frame)

print("Image saved as image.jpg")
```
# Schematics
![Headstone Image](IMG_0160.jpg)


# Bill of Materials
Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs.

| **Part** | **Note** | **Price** | **Link** |
|:--|:--|:--:|:--:|
| Raspberry Pi Kit | What the item is used for | 96.79 | [Link](https://www.amazon.com/RasTech-Raspberry-Starter-Heatsink-Screwdriver/dp/B0C8LV6VNZ/ref=sr_1_4?crid=3506HY00MCGVM&keywords=raspberry%2Bpi%2Bkit&qid=1718848547&s=electronics&sprefix=rasbperry%2Bpi%2Bkit%2Celectronics%2C83&sr=1-4&th=1) |
| Picam w stand | What the item is used for | 10.99 | [Link](https://www.amazon.com/Arducam-Raspberry-Camera-Module-1080P/dp/B07RWCGX5K/ref=sr_1_10?crid=1U9IECPRDX3WW&keywords=arducam%2Bpicam&qid=1747573778&s=electronics&sprefix=arducam%2Bpicam%2Celectronics%2C89&sr=1-10&th=1) |
| Speaker | Output speech for TTS | 9.99 | [Link](https://www.amazon.com/Mobile-Speaker-Compact-Adhesive-Installation/dp/B0D95ZYCW6/ref=sr_1_21?crid=369CH18NKBSVU&keywords=speakerphone%2Bsmall%2Baudio%2Bjack&qid=1747574092&sprefix=speakerphone%2Bsmall%2Baudio%2Bjack%2B%2Caps%2C85&sr=8-21&th=1) |
| Microphone | Input sound/words using camera for STT | 9.99 | [Link](https://www.amazon.com/DUNGZDUZ-Microphone-Computer-Sensitivity-Mini-Sized/dp/B0CNVZ27YH/ref=sr_1_7?crid=2E8AID5UQ1ZZZ&keywords=usb+microphone&qid=1747574148&sprefix=usb+microphone+%2Caps%2C143&sr=8-7) |
| RPI Camera Flash Module | Upgrade from my previous camera | 23.99 | [Link](https://www.amazon.com/dp/B07X1VGQSL?psc=1&smid=A2IAB2RW3LLT8D&ref_=chk_typ_imgToDp) |
# Other Resources/Examples

- [VOSK MODELS](https://alphacephei.com/vosk/models)
- [RASPBERRY PI IMAGER](https://www.raspberrypi.com/software)
- [PIPER TTS-PYTHON API DOCUMENTATION](https://github.com/OHF-Voice/piper1-gpl/blob/main/docs/API_PYTHON.md)
- [pyttsx3 Documentation](https://pypi.org/project/pyttsx3)
