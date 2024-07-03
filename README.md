# AI-Trainer
Using computer vision and machine learning to correct improper weightlifting form.
# Abstract:
Lifting weights is a crucial part of any effective exercise routine, yet improper technique can lead to injuries. To address this, I propose a system that detects and suggests improvements for form in the three key compound exercises: barbell bench press, squat, and deadlift. My approach first identifies the exercise being performed using a convolutional neural network (CNN), then utilizes a pre-trained human pose CNN to estimate the positions of the user's joints. By analyzing the relative positions of these joints, I detect any significant deviations. The system then provides feedback to the user on how to correct their form. My experiments with various training datasets have resulted in a model with an approximately 80% classification accuracy. However, the limited availability of robust open-source weightlifting datasets poses a challenge. Additionally, while human pose estimation shows promise for form detection, further calibration is needed to ensure the system's performance is consistent regardless of camera angle.
# Introduction:
# Approach:
# Part 1: Image Classification
# Part 2: Human Pose Estimation
# Part 3: Form Feedback


