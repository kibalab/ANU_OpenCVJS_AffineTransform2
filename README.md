
## 소감
>이번에 OpenCV.js에서 Perspectiv Transform와 Image Threshold, Crop을 이용한 A4페이지 캡쳐 후처리 기능을 작성해보았습니다.
이전에 수행한 과제와 다소 비슷한 부분이 있었지만 실제로 해볼려고 하니 Perspectiv Transform를 동작하기위한 행렬 작성에 어려움을 겪었습니다. 하지만 여러번의 시도 끝에 깨끗하게 영역을 잘라낼 수 있어서 너무 뿌듯했습니다.
이번 퀴즈로 이미지를 잘라서 저장하는 과정의 동작을 좀 더 자세히 알고 직접 만들수 있게 되어서 너무 기쁩니다. 앞으로 이런 변형을 활용하여 좀 더 신기하고 신박한 기능들을 만들어나가고싶다고 생각했습니다.

## 소스 코드
```
let src = cv.imread('canvasInput');
let dst = new cv.Mat();
let dsize = new cv.Size(src.rows*2, src.cols*2);
let center = new cv.Point(src.cols / 2, src.rows / 2);
// You can try more different parameters
let M = cv.getRotationMatrix2D(center, -339, 1);
cv.warpAffine(src, dst, M, dsize, cv.INTER_LINEAR, cv.BORDER_CONSTANT, new cv.Scalar());
let srcTri = cv.matFromArray(3, 1, cv.CV_32FC2, [0, 0.04, 0.48, 0.9, 0.86, 0.12]);
let dstTri = cv.matFromArray(3, 1, cv.CV_32FC2, [0, 0.21, 0.64, 1.64, 1.4, 0.6]);
M = cv.getAffineTransform(srcTri, dstTri);
cv.warpAffine(dst, dst, M, dsize, cv.INTER_LINEAR, cv.BORDER_CONSTANT, new cv.Scalar());

cv.cvtColor(dst, dst, cv.COLOR_RGBA2GRAY, 0);
cv.threshold(dst, dst, 158, 255, cv.THRESH_BINARY);
let rect = new cv.Rect(45, 170, src.cols/1, src.rows/1);
dst = dst.roi(rect);
cv.imshow('canvasOutput', dst);
src.delete(); dst.delete(); M.delete();
```
