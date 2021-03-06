## png2gif
```
import imageio
import os
images = []
path = r"C:\Users\CYD\Documents\NB_COPY\GAN_Models\WGAN\Conditional-WassersteinGAN-master
\Inproved_rgan\RGAN\Experient_Comic\spec_rgan"
filenames = os.listdir(path)
for num, filename in enumerate(filenames):
    if num % 10 == 0:
        images.append(imageio.imread(os.path.join(path, filename)))
imageio.mimsave(r'C:\Users\CYD\Desktop\comic.gif', images, duration=0.25)

```

GOTO [here](http://pillow.readthedocs.io/en/3.1.x/reference/Image.html)

Convertion between variou format
===================================
	
## Convert between Python tuple and list
```
a = (1, 2)      # a is a tuple 
b = list(a)     # b is a list 
c = tuple(b)  # c is a tuple 
```
## Convert between Python tuple, list and NumPy 1D array 
```
a = (1, 2)          # a is a tuple 
b = np.array(a)  # b is an numpy array 
c = tuple(b)       # c is a tuple 

a = [1, 2]          # a is a python array 
b = np.array(a)  # b is a numpy array 
c = list(b)          # c is a python list 
```
## Convert between 2d List and 2d numpy array
Just pass the list to np.array
```
a = [[1, 2, 3], [4, 5, 6], [7, 8, 9]] 
```
```
a = np.array(a)
```
	
If the sub-arrays do not have the same length, this solution will only give you a numpy array of lists (i.e. the inner lists won't be converted to numpy arrays)
[Instead there are 3 options:](https://stackoverflow.com/questions/10346336/list-of-lists-into-numpy-array)

1) Make an array of arrays:
```
x=[[1,2],[1,2,3],[1]]
y=numpy.array([numpy.array(xi) for xi in x])
type(y)
>>><type 'numpy.ndarray'>
type(y[0])
>>><type 'numpy.ndarray'>
```
2) Make an array of lists:
```
x=[[1,2],[1,2,3],[1]]
y=numpy.array(x)
type(y)
>>><type 'numpy.ndarray'>
type(y[0])
>>><type 'list'>
```
3) First make the lists equal in length:
```
x=[[1,2],[1,2,3],[1]]
length = len(sorted(x,key=len, reverse=True)[0])
y=numpy.array([xi+[None]*(length-len(xi)) for xi in x])
y
>>>array([[1, 2, None],
>>>       [1, 2, 3],
>>>       [1, None, None]], dtype=object)

```

## Convert between NumPy 2D array and NumPy matrix

```
a = numpy.ndarray([2,3])   # create 2x3 array
m1 = numpy.asmatrix(a)   # does not create new matrix, m1 refers to the same memory as a 
m2 = numpy.matrix(a)      # creates new matrix and copies content 

b1 = numpy.asarray(m2)   # does not create array, b1 refers to the same memory as m2
b2 = numpy.array(m2)      # creates new array and copies content 
 ```

## Read/Write Images with OpenCV
```
image = cv.LoadImage(“ponzo.jpg”)
cv.SaveImage(“out.png”, image)
```
## Read/Write Images with PIL
```
image = Image.open(“ponzo.jpg”)
image.save(“out.jpg”)
```
## Read/Write Images with PyOpenCV
```
mat = pyopencv.imread(“ponzo.jpg”)
pyopencv.imwrite(“out.png”, mat)
``` 
 	
#Convert between OpenCV image and PIL image

## color image 
```
cimg = cv.LoadImage("ponzo.jpg", cv.CV_LOAD_IMAGE_COLOR)     # cimg is a OpenCV image
pimg = Image.fromstring("RGB", cv.GetSize(cimg), cimg.tostring())    # pimg is a PIL image 
cimg2 = cv.CreateImageHeader(pimg.size, cv.IPL_DEPTH_8U, 3)      # cimg2 is a OpenCV image 
cv.SetData(cimg2, pimg.tostring())
```
Note: OpenCV stores color image in BGR format. So, the converted PIL image is also in BGR-format. The standard PIL image is stored in RGB format. 

## gray image 
```
cimg = cv.LoadImage("ponzo.jpg", cv.CV_LOAD_IMAGE_GRAYSCALE)   # cimg is a OpenCV image 
pimg = Image.fromstring("L", cv.GetSize(cimg), cimg.tostring())                 # pimg is a PIL image 
cimg2 = cv.CreateImageHeader(pimg.size, cv.IPL_DEPTH_8U, 1)              # cimg2 is a OpenCV image
cv.SetData(cimg2, pimg.tostring())
 ```
 	
## Convert between PIL image and NumPy ndarray
```
image = Image.open(“ponzo.jpg”)   # image is a PIL image 
array = numpy.array(image)          # array is a numpy array 
image2 = Image.fromarray(array)   # image2 is a PIL image 
```
## Convert between PIL image and PyOpenCV matrix
```
image = Image.open(“ponzo.jpg”)                  # image is a PIL image
mat = pyopencv.Mat.from_pil_image(image)  # mat is a PyOpenCV matrix 
image2 = mat.to_pil_image()                        # image2 is a PIL image 
 ```
## Convert between OpenCV image and NumPy ndarray
```
cimg = cv.LoadImage("ponzo.jpg", cv.CV_LOAD_IMAGE_COLOR)   # cimg is a OpenCV image 
pimg = Image.fromstring("RGB", cv.GetSize(cimg), cimg.tostring())  # pimg is a PIL image 
array = numpy.array(pimg)     # array is a numpy array 
pimg2 = cv.fromarray(array)    # pimg2 is a OpenCV image
```
