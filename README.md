# 360videoTools:
base code fork自https://github.com/humek/omnieval
依赖: openCV 3.1
重构了代码结构，源代码只能gcc编译，建立了vs工程。为便于比较，master第一个commit直接是源代码，不能编译通过。加入了多种mapping以及支持rotate的操作
#Usage:
支持remap与comapre S-PSNR/L-PSNR两种操作
##TAppRemap: 
`TAppRemap.exe [-i input] [-o output] [-f filter] [-m input_height] [-b input_width] [-n output_height] [-v output_width] src dst  [-c rotx -d roty] [-e file.txt] [-g 1] [-u 1]`

 -i ... Input  file type, common: rect  eqar  cube                [rect]

***added:** aitoff, sanson, two(used for mapping)  poletop, poledown(used to get the pole of the top/down of rect) recttop_inv, rectdown_inv (used for inv)* 
***not used:** dyad, mult, bmul, trec, brec, grid, beqr, teqr, merc, cos2*

-o ... Output file type: cube, rect, eqar, merc, view             [rect]

-f ... Filter type: nearest, linear, bicubic                   [bicubic]

-m ... Input  height list                                          [500]

-b ... Input  width                                                 [2m]

-n ... Output height                                               [500]

-v ... Output width                                                 [2n]

-w ... Viewport width                                              [200]

-h ... Viewport height                                             [200]

-x ... Viewport fov x in degree                                     [90]

-y ... Viewport fov y in degree                                     [90]

-p ... Viewport center position phi (degrees)                        [0]

-l ... Viewport center position theta (degrees)                        [0]

-t ... Tracking data file                                         [none]\n"

-y ... Blend data together (only works with orec, etc ...)         [off]

-z ... Number of frames                                            [MAX]

-c ... rotation of x                                                       [0]

-d ... rotation of y                                                       [0]

-e ... file describe rotation 

-g ... is first frame rotate                                           [0]

-u ... is inv rotate  mapping                                       [0]

Example:

Remap:

TappRemap.exe -i rect -o aitoff -m 2048 -b 4096 -n 1024 -v 2048 -z 10 input.yuv aitoffOut_Rotate.yuv -c 0.8 -d 1.0 -g 1

TappRemap.exe -i rect -o cube -m 2048 -b 4096 -n 512 -v 512 -z 10 input.yuv cube.yuv

TappRemap.exe -i rect -o poledown -m 2048 -b 4096 -n 512 -v 512 -z 10 input.yuv poleOut.yuv

Inv Remap:
TappRemap.exe -i aitoff -o rect -m 1024 -b 2048 -n 2048 -v 4096 -z 10 aitoffOut_Rotate.yuv invRect.yuv -c 0.8 -d 1.0 -g 1 -u 1

TappRemap.exe -i poledown -o rectdown -m 512 -b 512 -n 512 -v 4096 -z 10 poleOut.yuv rectInv.yuv

.\TAppCompare.exe -i rect -o rect -m 2048 -b 4096 -n 2048 -v 4096 -z 1 "D:\Sequence\VR\Seq1.yuv" d:\out.yuv  sphere_655362.txt
