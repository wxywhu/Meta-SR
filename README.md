# Meta-SR
    参考图片 
    ![image](https://github.com/wxywhu/Meta-SR/blob/master/Figure1.png)
    核心：对于重建图（SR）中的每一点像素值 认为是由对应低分辨率特征图(FLR)上的相应像素位置的特征与一组卷积滤波器权重共同决定
    
    Location Projection: 寻找对应的决定像素点, SR中（i,j）除以缩放因子r,floor取整, 得到FLR中的位置（i',j'）
    
    Weight Prediction: 输入大小为 HWx3, 行向量由每个位置的取整偏差和缩放因子的倒数组成.以便同时训练多个缩放因子
                       输出为 HWx(inCxoutCxkxk),可理解为每个像素点对应一组权重
                       
    Feature Mapping: 输入为 FLR 大小 inCxinHxinW  权重大小：HWx(inCxoutCxkxk) 
                     两者按照像素位置对应相乘得到输出
                     输出为 SR 大小为：outCxHxW
                     
    关于相乘的理解：对于SR中的每个像素点 按照 Location Projection的方式在FLR找到对应像素点, 该像素点为中心的对应Kxk的区域（大小为inCxkxk）与权重inCxoutCxkxk 以卷积的方式（相乘求和）得到该像素点的值）
                 
