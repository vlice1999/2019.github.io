## 几个简单的例子
学习opencv的第一天，除了配置好opencv环境，只跟着课本测试了几个程序。现在感觉有点小兴奋，同时也有点小吃力，emmm~
### 显示图像
```cpp
#include "highgui.h"

int main(int argc, char** argv){
    IplImage* img = cvLoadImage(argv[1]);
    cvNamedWindow("Example1",CV_WINDOW_AUTOSIZE);
    cvShowImage("Example1",img);
    cvWaitKey(0);
    cvReleaseImage(&img);
    cvDestroyWindow("Example1");
}
```

### 播放avi视频
```cpp
#include "highgui.h"

int main(int argc, char** argv){
    cvNamedWindow("Example2",CV_WINDOW_AUTOSIZE);
    CvCapture* capture = cvCreateFileCapture(argv[1]);
    IplImage* frame;
    while(1){
        frame = cvQueryFrame(capture);
        if(!frame) break;
        cvShowImage("Example2",frame);
        char c = cvWaitKey(33);
        if(c == 27) break;
    }
    cvReleaseCapture(&capture);
    cvDestroyWindow("Example2");
}
```

### 视频播放控制（添加滚动条）
```cpp
#include <cv.h>
#include <highgui.h>

int g_slider_position = 0;
CvCapture* g_capture = NULL;

void onTrackbarSlide(int pos){
    cvSetCaptureProperty(
        g_capture,
        CV_CAP_PROP_POS_FRAMS,
        pos
    );
}

int main(int argc, char** argv){
    cvNamedWindow("Example3",CV_WINDOW_AUTOSIZE);
    g_capture = cvCreateFileCapture(argv[1]);
    int frames = (int) cvGetCaptureProperty(
        g_capture,
        CV_CAP_PROP_POS_FRAM_COUNT
    );
    if(frames != 0){
        cvCreateTrackerbar(
            "Position",
            "Example3",
            &g_slider_position,
            frames,
            onTrackbarSlide
        );
    }
    IplImage *frame;
    while(1){
        frame = cvQueryFrame(capture);
        if(frame == NULL) break;
        cvShowImage("Example3",frame);
        char c = cvWaitKey(33);
        if(c == 27) break;
    }
    cvReleaseCapture(&g_capture);
    cvDestroyWindow("Example3");
}
```
