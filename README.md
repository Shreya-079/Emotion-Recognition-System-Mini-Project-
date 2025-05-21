# Emotion-Recognition-System-Mini-Project-

import cv2
from keras.models import load_model
import numpy as np

#Load face detection and emotion model
face_cascade cv2.CascadeClassifier('haarcascade_frontalface_default.xml')
model load_model('emotion_model.hdf5', compile=False)

#Emotion labels
emotion_labels = ['Angry', 'Disgust', 'Fear', 'Happy', 'Sad', 'Surprise', 'Neutral']

#Open webcam

cap = cv2.VideoCapture(0)

while True:

ret, frame = cap.read()

if not ret:

break

gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)

# Convert to grayscale

faces = face_cascade.detectMultiScale (gray, scaleFactor=1.3, minNeighbors=5)

for (x, y, w, h) in faces:

roi gray gray[y:y+h, x:x+w] # Region of Interest (face)

#Resize face to 64x64

roi gray = cv2.resize(roi_gray, (64, 64), interpolation=cv2.INTER_AREA)
if np.sum(roi_gray) != 0: Check if the face region is not empty

roi roi gray.astype('float32') / 255.0

Normalize pixel values to [0, 1]

roi np.expand_dims(roi, axis-e)

Add batch dimension

roi np.expand_dims(roi, axis--1)

#Add channel dimension

#Predict the emotion

prediction model.predict(roi)[0]

label emotion_labels[np.argmax(prediction)]

Get the emotion with max probability

#Draw rectangle around the face and label the emotion

cv2.rectangle(frame, (x, y), (x+w, y + h), (255, 0, 0), 2)

cv2.putText(frame, label, (x, y 10), cv2.FONT_HERSHEY_SIMPLEX, 1, (8, 255, 0), 2, cv2.LINE_AA)

#Display the frame with the face and emotion label

cv2.imshow("Emotion Detector', frame)

if cv2.waitKey(1) & 0xFF == ord('q'): Press 'q' to quit

break

cap.release()

cv2.destroyAllwindows()
