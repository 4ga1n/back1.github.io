---
layout: post
title: "Opencv Java: transform 1 and 3 channels pics to 4 channels pics"
category: tools
---

I searched web for code that implements the function of transform 1 and 3 channels pics to 4 channels pics using java opencv, turned out that there is only c++ and python code available. So I found out how to do this in Java and shared here. 

```java
public static Mat convertTo4ChannelAndReleaseOld(Mat inputPicMat){
    if( inputPicMat.channels() == 3 ){
        List<Mat> srcList=new ArrayList<Mat>();
        List<Mat> dstList=new ArrayList<Mat>();

        Mat convertedPicMat = new Mat(inputPicMat.size(), CvType.makeType(inputPicMat.depth(),4));

        int[] from_to = { 0,0, 1,1, 2,2, 2,3 };
        MatOfInt fromto = new MatOfInt(from_to);

        srcList.add(0,inputPicMat);
        dstList.add(0,convertedPicMat);
        Core.mixChannels(srcList,dstList, fromto);
        inputPicMat.release();
        return convertedPicMat;
    }else if (inputPicMat.channels() == 1){
        List<Mat> srcList=new ArrayList<Mat>();
        List<Mat> dstList=new ArrayList<Mat>();

        Mat convertedPicMat = new Mat(inputPicMat.size(), CvType.makeType(inputPicMat.depth(),4));

        int[] from_to = { 0,0, 0,1, 0,2, 0,3 };
        MatOfInt fromto = new MatOfInt(from_to);

        srcList.add(0,inputPicMat);
        dstList.add(0,convertedPicMat);
        Core.mixChannels(srcList,dstList, fromto);
        inputPicMat.release();
        return convertedPicMat;
    }else{
        return inputPicMat;
    }
}
```