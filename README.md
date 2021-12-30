# face-rec
this is the code for face recognition with python (and maybe future opencv)

#>starting here>the code>#

import cv2
import face_recognition
import sys

def take_pic():
    print("please wait while we scan your face...")
    cap = cv2.videoCapture(0)
    ret, frame = cap.read()
    cv2.inwrite('picture.jpg', frame)
    cv2.destroyAllWindows()
    cap.release()
    print("face scan complete")

def analyze_user():
    print("please wait while we analyze your face...")
    baseimg = face_recognition.load_image_file("me.jpg")
    baseimg = cv2.cvtColor(baseimg, cv2.COLOR_BGR2RGB)

    myface = face_recognition.face_location(baseimg)[0]
    encodemyface = face_recognition.face_encodings(baseimg)[0]
    cv2.rectangle(baseimg, (myface[3], myface[0]), (myface[1], myface[2]), (255, 0, 255), 2)

    cv2.imshow("Test", baseimg)
    cv2.waitkey(0)

    sampleimg = face_recognition.load_image_file("picture.jpg")
    sampleimg = cv2.cvtColor(sampleimg, cv2.COLOR_BGR2RGB)

    samplefacetest = face_recognition.face_location(sampleimg)[0]
    try:
        encodesamplefacetest = face_recognition.face_encodings(sampleimg)[0]
    except IndexError as e:
        print("authenication fail, error: ERR_INDEX")
        sys.exit()

    result = face_recognition.compare_faces([encodemyface]. encodesamplefacetest)
    resultstring = str(result)


    if resultstring == "[True]":
        print("authanication succes! welcome back!")
    else:
        print("authanication fail, error: UNKNOWN. see you again!")

take_pic()
analyze_user()
#>ending here>the code>#

#you are welcome
