# AI-Trainer

Using computer vision and machine learning to correct improper weightlifting form.

# Abstract:

Lifting weights is a crucial part of any effective exercise routine, yet improper technique can lead to injuries. To address this, I propose a system that detects and suggests improvements for form in the three key compound exercises: barbell bench press, squat, and deadlift. My approach first identifies the exercise being performed using a convolutional neural network (CNN), then utilizes a pre-trained human pose CNN to estimate the positions of the user's joints. By analyzing the relative positions of these joints, I detect any significant deviations. The system then provides feedback to the user on how to correct their form. My experiments with various training datasets have resulted in a model with an approximately 80% classification accuracy. However, the limited availability of robust open-source weightlifting datasets poses a challenge. Additionally, while human pose estimation shows promise for form detection, further calibration is needed to ensure the system's performance is consistent regardless of camera angle.

# Introduction:

Most weightlifting injuries result from using incorrect form while performing exercises. The barbell bench press, squat, and deadlift—referred to as the "big three"—are particularly popular among strength enthusiasts. However, these exercises are also among the easiest to perform improperly, making them potentially dangerous. My goal with this project is to develop a solution that helps users correct their form and learn to perform these lifts correctly.

Incorrect form has become a more significant issue following COVID. Gyms are hotspots for viral transmission, leading many beginners to start their fitness journeys at home. Without feedback from a personal trainer and minimal prior experience, learning to lift weights properly can be quite challenging. While commercial solutions like Peloton ($2000), Tonal ($3000), and MIRROR ($1500) exist for interactive at-home exercise, none offer real-time feedback except for MIRROR, which charges an additional $40 per session with a live trainer. Moreover, none are specifically designed for addressing free weights.

The proliferation of machine learning research over the past decade has also impacted exercise science. Researchers have developed models to tackle exercise classification and form detection issues. One example is GymCam, which detects, recognizes, and tracks simultaneous exercises in unconstrained scenes. Khurana et al. used “frequency-based feature matching” that employs human pose estimation to track joint movements, identifying exercises based on joint trajectory and frequency sampling. Another example is Pose Trainer, a tool for correcting exercise posture using pose estimation, evaluating form based on joint angles and distances, and using thresholds to identify improper movements.

While Pose Trainer’s function is similar to my goal, it focuses on minor bodily tendencies for niche exercises like bicep curls and shoulder shrugs—known as isolation exercises—which involve only a single joint. The risk of injury performing these movements is relatively small. By focusing on isolation exercises, Pose Trainer can analyze the movement of a single joint, making angle and position analysis straightforward.

My approach is more holistic. Instead of focusing on one or two specific joints, I evaluate the positions of multiple joints relative to each other to provide feedback based on the exercise being performed. Using a Human Pose Estimation model, I track these joints and find relations between them based on known bad form tendencies. Misaligned joints or incorrect distances between them can significantly increase the risk of long-term injury. By identifying these high-level form breakdowns that beginner lifters often overlook, I aim to mitigate potential future injuries.

# Approach:

# Part 1: Image Classification

The first part of my solution involves classifying images. Initially, I aimed to develop a library of human poses corresponding to each exercise, intending to use an image comparison algorithm such as shortest squared distance or structural similarity measure between joints to find the closest match for an input image. However, preliminary testing showed this approach was inconsistent, likely due to camera angle variance. Additionally, the barbell's position relative to the body proved more significant for classification than anticipated. For example, in the bench press, users extend their arms fully, similar to the deadlift, leading to confusion when cross-correlating joints across different exercises.

Due to these issues, I pivoted to a brute-force categorical convolutional neural net (CNN), built using TensorFlow and Keras with the following architecture:

-----------------------------ADD IMAGE HERE-----------------------------------

Using the Bing Web Search API, I scraped 250 images for each chosen exercise: barbell bench press, barbell back squat, and barbell deadlift. After manually filtering out faulty representations and fixing formatting issues, the model achieved ~80% accuracy, prompting me to proceed with using a CNN for classification.

Given the limited size of the initial dataset, I sought to improve accuracy by gathering more images. However, finding high-quality images online proved challenging, as scraping search engines yielded increasingly lower quality results over time. Therefore, I created my own dataset, capturing over 1000 images for each exercise using four different subjects of varying races to mitigate potential bias. This substantial increase in image count was taxing on my computational resources. Finally, I decided to experiment with training the model on a dataset composed entirely of Human Pose Estimation (HPE) output to see what results it would yield.

# Part 2: Human Pose Estimation

# Part 3: Form Feedback
