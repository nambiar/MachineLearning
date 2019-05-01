#### What are Channels and Kernels

Channels in any image processing or Machine learning refers to a group of datasets/image/sets which contains information of same type . For example in a image on a Red Channel we get a extracted version of image pixel containing values/brightness of color Red . On a gray scale channel we get the pixel value for color black and white.

Kernels provide a region (3x3) in our case where variations of pixel value can be accommodated i.e if to extract a edge from an image . We take a 3*3 region/matrix where the pixels are bright on left part and dark on right part which when imposed on image gives us edge in that region . So in short kernels helps us in extraction features from an image.

#### Why should we only (well mostly) use 3x3 Kernels?

3x3 kernels provide symmetry which is used in any feature extraction. 2X2 cannot provide that.

As with the inference that scaling of an image does not throw away its loudest feature . 3x3 which means extracting 9 parameters can easily understand feature in a 5x5 image , rather than employing a 5x5 kernel which would take up 25 parameters   and thus reducing computation.

Hardware accelerators provided on GPUs for t3x3 matrix which helps in easy computation. For doing a 7x7 feature kernel can be easily split up by doing a 3x3 kernels thrice.

#### 199x199 - 1x1

199x199- 197x197- 195x195- 193x193- 191x191- 189x189- 187x187- 185x185- 183x183- 181x181- 179x179- 177x177- 175x175- 173x173- 171x171- 169x169- 167x167- 165x165- 163x163- 161x161- 159x159- 157x157- 155x155- 153x153- 151x151- 149x149- 147x147- 145x145- 143x143- 141x141- 139x139- 137x137- 135x135- 133x133- 131x131- 129x129- 127x127- 125x125- 123x123- 121x121- 119x119- 117x117- 115x115- 113x113- 111x111- 109x109- 107x107- 105x105- 103x103- 101x101- 99x99- 97x97- 95x95- 93x93- 91x91- 89x89- 87x87- 85x85- 83x83- 81x81- 79x79- 77x77- 75x75- 73x73- 71x71- 69x69- 67x67- 65x65- 63x63- 61x61- 59x59- 57x57- 55x55- 53x53- 51x51- 49x49- 47x47- 45x45- 43x43- 41x41- 39x39- 37x37- 35x35- 33x33- 31x31- 29x29- 27x27- 25x25- 23x23- 21x21- 19x19- 17x17- 15x15- 13x13- 11x11- 9x9- 7x7- 5x5- 3x3- 1x1

91 times can do the same by the python code 

`i = 199
for i in range(199,1,-2):
	print (str(i) + "x" + str(i) +"-"),`