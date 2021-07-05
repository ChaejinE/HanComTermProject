import cv2
import numpy as np

capture = cv2.VideoCapture("1.avi")
while True:
	ret, frame = capture.read()

	hsv = cv2.cvtColor(frame, cv2.COLOR_BGR2HSV)
	lower_white = np.array([0,0,60])
	upper_white = np.array([179,255,200])
	mask= cv2.inRange(hsv,lower_white, upper_white)
	roi = mask[430:450, :]
	stop_roi = mask[430:450, :]

	cv2.namedWindow('roi_view')
	cv2.moveWindow('roi_view', 800, 200)

#차선검출
	lane=[0,0]
	for i in range(0,120,10):
		lane_mask = mask[435:445, i:i+20]
		for j in range(0,9):
			for k in range(0,19):
				if lane_mask[j,k]==255:
					lane[0]=lane[0]+1;
		if lane[0]>150:
			lane[0]=i
			break
		else:
			lane[0]=0
	roi=cv2.cvtColor(roi,cv2.COLOR_GRAY2BGR)
	roi=cv2.rectangle(roi, (lane[0],4), (lane[0]+20,14), (0,255,0),3)

	for i in range(520,619,10):
		lane_mask = mask[435:445, i:i+20]
		for j in range(0,9):
			for k in range(0,19):
				if lane_mask[j,k]==255:
					lane[1]=lane[1]+1;
		if lane[1]>150:
			lane[1]=i
			break
		else:
			lane[0]=0
	roi=cv2.rectangle(roi, (lane[1],4), (lane[1]+20,14), (0,255,0),3)
	
#정지선 검출
	stop_roi_mask = stop_roi[2:15, 120:520]
	cnt_stop = cv2.countNonZero(stop_roi_mask)
	print(cnt_stop)
	if cnt_stop > 2400:
		for i in range(0,19):
			for j in range(120,520):
				if stop_roi[i,j]==255:
					roi[i,j]=[0,212,255]
	
	cv2.imshow('roi_view',roi)
	cv2.imshow('frame', frame)

	if cv2.waitKey(1) >0:
		break

cap.release()
cv2.waitKey(0)
cv2.destroyWindow("frame")
cv2.waitKey(0)
cv2.destroyAllWindows()
	
