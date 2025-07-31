# Optical Character Recognition
Replace this text with a brief description (2-3 sentences) of your project. This description should draw the reader in and make them interested in what you've built. You can include what the biggest challenges, takeaways, and triumphs from completing the project were. As you complete your portfolio, remember your audience is less familiar than you are with all that your project entails!

You should comment out all portions of your portfolio that you have not completed yet, as well as any instructions:
```HTML 
<!--- This is an HTML comment in Markdown -->
<!--- Anything between these symbols will not render on the published site -->
```

| **Engineer** | **School** | **Area of Interest** | **Grade** |

| Charles L. | Roslyn High school | Civil/ Environmental engineering | Rising Junior |

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)
  
# Final Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your final milestone, explain the outcome of your project. Key details to include are:
- What you've accomplished since your previous milestone
- What your biggest challenges and triumphs were at BSE
- A summary of key topics you learned about
- What you hope to learn in the future after everything you've learned at BSE



# Second Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/y3VAmNlER5Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your second milestone, explain what you've worked on since your previous milestone. You can highlight:
- Technical details of what you've accomplished and how they contribute to the final goal
- What has been surprising about the project so far
- Previous challenges you faced that you overcame
- What needs to be completed before your final milestone 

# First Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/CaCazFBhYKs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your first milestone, describe what your project is and how you plan to build it. You can include:
- Raspberry pi 4
      - Used raspberry pi imager to install the OS onto the sd card
      - Connected the camera to it
- SSH file: protocol allowing 2 computers to communicate
        - Downloaded packages which allowed me to use the camera
        - camera.py
This script uses the Raspberry Pi camera to make an image and save it. It uses libraries to handle the capture and storage of the image.

- OCR/ Optical Character Recognition
      - Installed the tesseract library which would allow the program to extract text from images
  
  sudo apt install tesseract-ocr
      - This script processes an image using various different techniques in order to detect and highlight readable text, then saves the results. It makes use of image processing and OCR tools to extract and display the text visually. This script makes the process extremely easy. 

- Technical progress you've made so far
- Challenges you're facing and solving in your future milestones
- What your plan is to complete your project

# Schematics 
Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. 

# Code
Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. 

```c++
void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);
  Serial.println("Hello World!");
}

void loop() {
  // put your main code here, to run repeatedly:

}
```

# Bill of Materials
Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs. 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Raspberry Pi Kit | What the item is used for | 96.79 | <a href="https://www.amazon.com/RasTech-Raspberry-Starter-Heatsink-Screwdriver/dp/B0C8LV6VNZ/ref=sr_1_4?crid=3506HY00MCGVM&dib=eyJ2IjoiMSJ9._zkM62vSQ8p7tNr88715LdMv_qHh72Je-tkF9PXEa3chDE53QT4aZu4AGAb4ihE61QY4ZD55nKF6Fp2Kfs8t7AbafM_JrlJFfHo9OB4eAVGqa0EB-7aoBQHPmhKHZ2MW8ny-Kd44bMVlVxPlTWVk5YHIN5P3uKVqrE5Dcal0rKkHny-O6Xyb5ux2AOU6OwVbkag_bqBX66RQNRrgBuz-0pS43mcx93IZTQA9R8NaJJypYU2HAycp-XicTFmyU60a01Nfm9iuyo6B9yA8ppN3OQQyJ-NQ9xyNPxfTLwkqtng.yAYpU6outhQcZmOZhN9Wb6yTw7A85CNUbXZguGInZNg&dib_tag=se&keywords=raspberry%2Bpi%2Bkit&qid=1718848547&s=electronics&sprefix=rasbperry%2Bpi%2Bkit%2Celectronics%2C83&sr=1-4&th=1"> Link </a> |
| Picam w stand | What the item is used for | 10.99 | <a href="https://www.amazon.com/Arducam-Raspberry-Camera-Module-1080P/dp/B07RWCGX5K/ref=sr_1_10?crid=1U9IECPRDX3WW&dib=eyJ2IjoiMSJ9.EQptXsj1i39Y9oggTYxdai89FVefBqmO-xGB4sBBTHO4SEXcCZUKpLs1pTfSI2UV6zy9s3AQs7Evflr1mgvYz1YCSz3mqc1fKoWJuY2h_sLEdwqeJmnuUHIk2vmkOBLRlXijApDdRtOGjvFpd22kZibWh01QrWXaEwqpEp-2yRu8AwtKM3-xvdpkUNxIUIbjqrSK_cZ26yCkFh88Ih6aKDnMHVzWvkGv8cZGmAsc7eT7RKndhuCD03QQCco8ZhufAfPk0RJ-nafMKigKik2-9dEEZYTcX1D5vsv4x-weTH8.wWxtDi-AjBJ6-FuY_isVSX857HXALzCvS0vuocOJ6xg&dib_tag=se&keywords=arducam%2Bpicam&qid=1747573778&s=electronics&sprefix=arducam%2Bpicam%2Celectronics%2C89&sr=1-10&th=1"> Link </a> |
| Speaker | What the item is used for | 9.99 | <a href="https://www.amazon.com/Mobile-Speaker-Compact-Adhesive-Installation/dp/B0D95ZYCW6/ref=sr_1_21?crid=369CH18NKBSVU&dib=eyJ2IjoiMSJ9.fGxmsmnwIDfWJ86jFkBj2M9zmcDcTJDJ5mrEoKbPoNrsWxuJa_dYL6qoeEOWDCdistvn0ql7KvLvdE5jqDr0-IY9Hn9YsWu1Oy3eXWFB1iXZCoK66NzPfzialhjLhJGKAL7YU3iBTpfb7gJ5oM3pnHuzh9tfRA-QkKQPcTNZS39EEGN-fitqnkFQOGbfjIMaJcyEuFZuUIz8bj94BBA1-cHcB6OZ-uoxfiZAST_tFX8.8v-xvor8mw64ExKDR3N29OV45k1u_23oDE4b4od7GiM&dib_tag=se&keywords=speakerphone%2Bsmall%2Baudio%2Bjack&qid=1747574092&sprefix=speakerphone%2Bsmall%2Baudio%2Bjack%2B%2Caps%2C85&sr=8-21&th=1"> Link </a> |
| Microphone | What the item is used for | 9.99 | <a href="https://www.amazon.com/DUNGZDUZ-Microphone-Computer-Sensitivity-Mini-Sized/dp/B0CNVZ27YH/ref=sr_1_7?crid=2E8AID5UQ1ZZZ&dib=eyJ2IjoiMSJ9.ALlacqVSJFYCMwk0BLBt4BE78M6dbL4aQxGWFHFGViY7QOzmOSfkxRzzMD4BytGFdvrXnYFwbFQpiWeLB37vgMOeTgeyNJDCEdkcPjHzzHRJxfNFVUN6RfiMHaRcFDG-9Bv_yfPh1GhToIG1whgMGesfk7lXYtf8SFgQiEq2amOZxI0tqGpX2VQclkxKSnqhF6yzTiCWcZ4eNLkG1Dd01JochzymYWm59TYI_ipygVEt9UpdCReF2L_Ap0gIyhTLupQRKLocdolLZufM8LKLonKajGSQwrgEu_3jmlV10mM.wRiTmzhi2KBZXCOWVMCU_b0r9fvSClHWCv29BKgVQ4o&dib_tag=se&keywords=usb+microphone&qid=1747574148&sprefix=usb+microphone+%2Caps%2C143&sr=8-7"> Link </a> |
# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.
