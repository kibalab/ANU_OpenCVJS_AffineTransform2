
## 김진혁 학생(조장) 소감
>이번에 OpenCV.js에서 Affine Transform을 사용한 Crop이미지처리를 수행해보고 Matrix가 이미지 처리 분야에 어떻게 활용되는지 알아보았습니다. 처음에는 너무 어렵게 생각해서 조금 해매었지만 심재창 교수님의 수업을 통해 배운 내용을 생각해보니 금방 해결방법을 생각해서 해결할수 있었습니다.
이번 과제로 종이를 번역하거나 잘라서 저장하는 어플리케이션은 어떻게 동작하는지 일부를 이해할수 있게 되어서 너무 기쁩니다. 앞으로 이런 변형을 활용하여 좀 더 신기하고 신박한 기능들을 만들어나가고싶다고 생각했습니다.

## 남태승 학생 소감
>이번 과제를 진행하면서 기하학적 변환을 통한 영상처리 분야의 효과에 대해서 알아보고 이를 코드로 구현하여 보았습니다. 직접 이미지를 입력하여 입력된 이미지와 출력된 이미지를 비교하여보니 변환 후의 이미지가 반듯하여 보기에도 좋았습니다. 이런 실습을 통하여 디지털 영상처리의 기하학적 변환에 대해서 좀 더 이해한 것 같아서 너무 기쁩니다. 물론 변환 과정을 코드로 구현하는 부분이 조금 어려웠지만 결과적으로 완성되어 너무 즐겁습니다.

## 소스 코드
```
let src = cv.imread('canvasInput');
let dst = new cv.Mat();
let dsize = new cv.Size(src.rows*2, src.cols*2);
let center = new cv.Point(src.cols / 2, src.rows / 2);
// You can try more different parameters
let M = cv.getRotationMatrix2D(center, 338, 1);
cv.warpAffine(src, dst, M, dsize, cv.INTER_LINEAR, cv.BORDER_CONSTANT, new cv.Scalar());
let rect = new cv.Rect(300, 620, 1000, 1400);
dst = dst.roi(rect);
cv.imshow('canvasOutput', dst);
src.delete(); dst.delete(); M.delete();
```
