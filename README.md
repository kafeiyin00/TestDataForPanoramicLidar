# TestDataForPanoramicLidar
A test data for fusion of panoramic images and point clouds collected by mobile mapping system

## Main description
This is a test data set collected by the Lynx mobile mapping system in Wuhan University.
The data contains panoramic images, laser point clouds, and original pos data.
Using the method proposed in

[Automatic registration of panoramic image sequence and mobile laser scanning data using semantic features, Jianping Li, Bisheng Yang, et.al. 2017, In ISPRS](https://www.sciencedirect.com/science/article/pii/S0924271617303829)

the boresight and level-arm parameters between laser scanner and panorama camera are estimated.
Then the laser point clouds are registered with the images for applications like detection,
recognition, and so on.

## Data
The orientation data is stored in the pos.txt file (Be careful that the Euler angles are defined in the NED coordinate system ).
The corresponding level arm parameter is (0,0,1.1), and boresight parameter is (-1.8, 177.7,-38.5).


## Example
To avoid the ambiguity,  here is a simple code, projecting the 3d point in the camera coordinate systme onto the panoramic image:

```
    ////////////////////////////////////////////////
    const int imageWidth = 4096;
    const int imageHeight = 2048;

    template <class T>
    void world2image(T &u, T &v, const T &x, const T &y, const T &z) {

        //bearing vector to theta phi
        double theta = atan2(y,x)/M_PI*180.0 + 180.0;
        double phi = atan2(sqrt(x*x+y*y),z)/M_PI*180.0;

        //theta phi to image coordinates
        u = T(imageWidth - (theta/360.0)*imageWidth);
        v = T(phi/180.0*imageHeight);
    }
    /////////////////////////////////////////////

```

And you will get this result:


If you use this data in your paper, please cite our work. :)

[Automatic registration of panoramic image sequence and mobile laser scanning data using semantic features, Jianping Li, Bisheng Yang, et.al. 2017, In ISPRS](https://www.sciencedirect.com/science/article/pii/S0924271617303829)
