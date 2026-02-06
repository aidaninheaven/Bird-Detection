# Bird-Detection

This is a guide on my bird detection program, using an open source AI model named YOLO, an image classification model using a built-in dataset.

For the required imports, it requires:
- cv2 -- This is what allows us to see and read the camera
- os -- allows us to grab directories from our device
- datetime -- used for timing the capture interval
- torch -- loads the AI model and lets it read
- smtplib -- handles the opening of the server which allows the script to send emails
- from email.message import EmailMessage -- function that allows the script to send an email
- from pathlib import Path -- allows us to track paths
- mimetypes -- allows us to see the extension of files (JPG, PNG, etc.)

From here, we load up the model via torch and set the confidence, iou, the class used from the dataset (in this case, 14 is the line for birds) and set it to evaluate

After, we setup the SMTP server and port (use the same one in the script) and set up an email. For the password, we need to create an app password, which you can use the internet to figure out.

After setting a couple of emails for recipients, we then set the image directory, which in my case is ~/images. the first time the script runs, it will create the directory.

for camera setup, we define the width and height, define the actual capture, and set the height, width and fps.

for tracking, we define save count, last save time, and the interval, which we can change the interval to any desired number.

for the loop, the model reads the capture, resizes the frame to the frame height and width for results checking, and a boolean is set to false for detected birds. however if a bird is found, the boolean is set to true and a rectangle is crated around the bird. we are able to add text above, in this case I only put "Bird".

we have another if statement underneath our loop, which it's condition is dependent on whether birds_detected is true. if it is, it'll track the current time, and if the time subtracted from the last save time is greater than the save interval, it will take an image and write it to the image directory.

below this, we have an if statement to break the loop by pressing Q.

in the cleanup section, which is triggered once the main loop is broken, it will stop capturing and destroy the window set by cv2.

for the email section,
