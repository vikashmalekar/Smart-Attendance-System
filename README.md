# Smart-Attendance-System
                                                                                                                                           
From the past few decades Face Recognition technology has made many improvements in the changing world in many areas. Using this face recognition system we can make the process of attendace posting system easy.                                                                                                                                                 
## Draw backs with Manual attendace Posting:
* Time consuming                                                                                                                                                               
* It can be easy to accidentally switch details and end up with false entry of data or in hand written briefings                                                               
* It takes more physical and mental effort to keep track of paper documents, to find information and to keep details correct                                                   
* Lack of security
The attendance posting throuugh face recogniton will overcome the above drawbacks
## Approach
### Step 1
Collecting all details of the people and updating in the database.                                                                         
For this purpose Sqlite is used.                                                                                                           
#### Sqlite:
SQLite is an in-process library that implements a self-contained, serverless, zero-configuration, transactional SQL database engine. It is a database, which is zero-configured, which means like other databases you do not need to configure it in your system.                     
                                                                                                                                           
SQLite does not require a separate server process or system to operate (serverless).                                                       
SQLite comes with zero-configuration, which means no setup or administration needed.
A complete SQLite database is stored in a single cross-platform disk file.
SQLite is very small and light weight, less than 400KiB fully configured or less than 250KiB with optional features omitted.               
SQLite is self-contained, which means no external dependencies.                                                                             
                                                                                                                                          The python Sqlite3 standard library is intended for working with databases which provides the sql interface.
                                                                                                                                        
studentdetails, attendance details, datetime tables are created. The studentdetails table stores the Id,name,rollno, branch,section.     
Attendace details tables has attendance details for all periods seperately. Datetime table has timestamp of when the attendance was posted for a particular period. 

### step 2
In this step the student details are entered into the data base. And the images of student are collected using opencv. The images are stored with the name as "student id + count" Example as 1.1,1.2,1.3 .... ,2.1,2.2,2.3....... etc. For each student the separate image folder is created.

### step 3
In this step we train the model. Here LBPH_Face_Recognizer is used to recognize images. This will be trained with the data of students.
####  LBPH Face Recognizer:
Local binary pattern is very simple and efficient algorithm used for face recognition.                                                                                           
Lets go deeply process of working of this algorithm.                                                                                                                             
Each image in the dataset will be in the form of a matrixes of pixels. We we sliding window technique. In this technique we will start from initial postion and take submatrix of size 3x3 and we do LBP operation                                                                                                                                                 
##### LBP operation:
  * Suppose we have a facial image in grayscale.
  * We can get part of this image as a window of 3x3 pixels.
  * It can also be represented as a 3x3 matrix containing the intensity of each pixel (0~255).
  * Then, we need to take the central value of the matrix to be used as the threshold.
  * This value will be used to define the new values from the 8 neighbors.
  * For each neighbor of the central value (threshold), we set a new binary value. We set 1 for values equal or higher than the threshold and 0 for values lower than the             threshold.
  * Now, the matrix will contain only binary values (ignoring the central value). We need to concatenate each binary value from each position from the matrix line by line into a new binary value (e.g. 10001101). Note: some authors use other approaches to concatenate the binary values (e.g. clockwise direction), but the final result will be the same.
Then, we convert this binary value to a decimal value and set it to the central value of the matrix, which is actually a pixel from the original image.
At the end of this procedure (LBP procedure), we have a new image which represents better the characteristics of the original image.
![image](https://user-images.githubusercontent.com/54492609/86869975-2c3df580-c0f5-11ea-911a-10cf4771892c.png)
##### Extracting Histograms:
Now, using the image generated in the last step, we can use the Grid X and Grid Y parameters to divide the image into multiple grids, as can be seen in the following image:
![image](https://user-images.githubusercontent.com/54492609/86870512-285ea300-c0f6-11ea-9175-961cfcf05819.png)

### step 4
In this step the video is captured from the PC cam using opencv. Now each frame of the video is considered as one image and given as input to the LBPH_face_recognizer model.
If the image is recognized then the attendance is posted in the database with time and period.
### Drawbacks:
--> It will fail in case of twins.                                                                                                                                               
--> It gives less accurate results in poor light conditions
                                                                                                                                          
                                                                                                                                        


                                                                                                                                            


