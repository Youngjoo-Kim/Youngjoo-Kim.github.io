---
title: "Intro to Visual SLAM"
date: 2019-11-01 20:30:00
categories: ROS Programming
---

##### **오늘은 Visual SLAM이 무엇인지에 대하여 세 가지 글을 읽어볼까 합니다 :)**

# 1) Introduction to SLAM
##### **: A very brief outline of simultaneous localisation and mapping**
## What is SLAM?
==**SLAM은 simultaneous localisation과 mapping을 나타내며 두 부분으로 구성된 모바일 로봇 공학에서 매우 중요한 문제를 해결하는 개념입니다.**==
- **Mapping :** 로봇이 있는 환경의 지도를 작성
- **Localisation :**로봇의 상대 위치 및 방향을 추적하면서 지도를 사용하여 환경을 탐색

SLAM 문제를 효과적으로 해결하면 자율 주행 자동차에서 로봇 청소기에 이르기까지 다양한 응용 프로그램을 갖춘 자율형(자체 제어식)모바일 로봇에서 많은 가능성이 열립니다.
이 문제를 해결하는 일반적인 방법은 '다중 오프셋 카메라', 'Depth 센서' 등을 사용하는 것을 포함하지만, 이곳에서는 단일 카메라만 사용하여 관찰되는 이미지를 분석하는 =="monocular SLAM"==에 중점을 둡니다.

SLAM 기술은 모바일 로봇뿐만 아니라 Snapchat의 얼굴 추적 필터 또는 SONY의 AR 효가와 같은 증강현실(AR)에도 적용될 수 있습니다.

## How visual SLAM works
SLAM의 작동 방식은 진행중인 프로세스의 네 가지로 나눌 수 있습니다.
==**1. Visual SLAM을 구현하는 첫 단계는 카메라에서 비디오의 이미지 프레임, 각 이미지에서 일반적으로 선 (예를 들면, 테이블 또는 벽의 가장자리)과 모서리와 같은 중요하고 뚜렷한 랜드마크를 식별하는 것입니다.**==

==**2. 환경이 각 프레임 사이에서 변하지 않는다고 가정하면, 연속 또는 가까운 프레임의 랜드마크는 카메라 환경의 3D 객체와 연관지어 집니다.**==

==**3. 그런 다음 랜드마크를 함께 표시하여 이미 본 물체와 다시 연관시킵니다.**== 데이터는 카메라의 위치(Localization : 현지화)와 환경지도(Mapping)에 대한 정보를 생성하는데 사용됩니다.

SLAM 알고리즘은 비디오 프레임과 랜드마크의 상당수 체인(Chain)을 통해 데이터를 사용하여 카메라가 이동한 경로의 추정치를 estimation합니다. 그리고 카메라가 관찰한 환경에서의 모든 물체와 특징의 3D 공간에서의 위치를 추정합니다. 또한, 환경의 다른 특징을 기준으로 카메라의 위치를 추정합니다.

일부 방법 및 알고리즘의 작동에서, 모바일 로봇이 자유롭게 로밍되고 상기 단계를 구현하기 전에, 환경에 관한 일부 초기 데이터가 프로세스를 시작하기 위해 주입될 수 있습니다.
단일 시각 카메라로 이러한 문제를 해결하기 위해 작동하는 다양한 알고리즘이 있습니다. (해당 웹사이트에 일부 참고 가능)

### The Extended Kalman Filter (EKF)
**모바일 로봇 공학과 관련된 많은 실제 factor들로 인해 환경의 3D 맵에서 랜드마크 및 객체 계산 오류는 불가피합니다.**
이는 수학적 오류의 축적, 분석된 비디오 프레임의 품질, 카메라 자체의 랜드마크 및 결함을 정확하게 식별하는데 어려움이 있기 때문입니다. **monocular SLAM에서 특히 중요한 문제는 '깊이 추정'입니다. 이를 고려한 방법이 ==EMF==이며 이것을 사용합니다.**

==**확장 칼만 필터 알고리즘은 지도에서 로봇의 위치와 랜드마크의 위치에 대한 불확실성을 추적합니다.**==
이 누적 데이터를 사용하여 로봇의 3D맵에서 로봇 및 객체의 위치에 대해서 업데이트 된, '최상의 추정치를 결정하는 계산을 수행'합니다. 이것은 로봇의 지도와 실제 환경 사이의 오류가 쌓이지 않고 "drift apart(떨어져)" 있다는 것을 의미합니다.


**- Reference list**

1.Riisgaard S, Blas MR. SLAM for dummies: A Tutorial approach to simultaneous localization and mapping by the ‘dummies’. [Online] Massachusetts Institute of Technology, 2005 [Accessed: 31st January 2016]. Available from: http://ocw.mit.edu/courses/aeronautics-and-astronautics/16-412j-cognitive-robotics-spring-2005/projects/1aslam_blas_repo.pdf [Accessed: 31st January 2016]
2.Bonin-Font F, Ortiz A, Oliver G. Visual navigation for mobile robots: A survey. [Online] Journal of Intelligent and Robotic Systems. Kluwer Academic Publishers; p. 263–296. Available from: http://dl.acm.org/citation.cfm?id=1452818 [Accessed: 31st January 2016]
3.Burbridge C, Spacek L, Condell J, Nehmzow U. Monocular Omnidirectional vision based robot Localisation and mapping. [Online] [Accessed: 31st January 2016]. Available from: https://www.cs.bham.ac.uk/~burbrcjc/papers/burbridge-etc08.pdf [Accessed: 31st January 2016]
4.Dyson Ltd. Dyson 360 EyeTM robot. [Online] Dyson. Dyson 360 EyeTM robot; Available from: https://www.dyson360eye.com [Accessed: 4th March 2016]
5.Malisiewicz T. The Future of Real-Time SLAM and ‘Deep Learning vs SLAM’. [Online] Tombone’s computer vision Blog. Available from: http://www.computervisionblog.com/2016/01/why-slam-matters-future-of-real-time.html [Accessed: 4th March 2016]
6.Royer E, Lhuillier M, Dhome M, Lavest J-M. Monocular vision for mobile robot localization and autonomous navigation. International Journal of Computer Vision. [Online] 2007;74(3): 237–260. Available from: http://maxime.lhuillier.free.fr/pIjcv07.pdf [Accessed: 31st January 2016]
7.Davison AJ. Real-time simultaneous Localisation and mapping with a single camera. [Online] [Accessed: 31st January 2016]. Available from: https://www.doc.ic.ac.uk/~ajd/Publications/davison_iccv2003.pdf [Accessed: 31st January 2016]
8.Neira JE, Ribeiro I, Tardd JD. Mobile robot localization and map building using Monocular vision. [Online] 2004 [Accessed: 31st January 2016]. Available from: http://webdiis.unizar.es/~jdtardos/papers/Neira_SIRS_1997.pdf [Accessed: 31st January 2016]
9.Klein G, Murray D. Parallel tracking and mapping for small AR Workspaces. [Online] 2007 Nov [Accessed: 27th February 2016]. Available from: http://www.robots.ox.ac.uk/~gk/publications/KleinMurray2007ISMAR.pdf [Accessed: 27th February 2016]
10.Davison AJ, Reid ID, Molton ND, Stasse O. MonoSLAM: Real-time single camera SLAM. IEEE Transactions on Pattern Analysis and Machine Intelligence. [Online] Institute of Electrical & Electronics Engineers (IEEE); 2007;29(6): 1052–1067. Available from: doi:10.1109/tpami.2007.1049
11.Leutenegger S. Group project supervision meeting. 11th February 2016.

[Reference Link](https://www.doc.ic.ac.uk/~ab9515/introductiontoslam.html)
- - -

# 2) Monocular Simultaneous Location and Mapping
### **: A guide to SLAM with only a single visual camera**
## Why is monocular SLAM important?
==**pure monocular SLAM이 사용되고 연구되는 주된 이유 중 하나는 이를 구현하는데 필요한 하드웨어가 훨씬 단순하기 때문입니다. 이것은 훨씬 저렴하고, 예를 들어 다른 시스템, 스테레오 SLAM보다 물리적으로 작은 것을 의미합니다.
그러나 단점은 monocular SLAM에 필요한 알고리즘이 훨씬 더 복잡하여, 소프트웨어가 훨씬 더 복잡하고 실질적이라는 것입니다.**==
단일 카메라의 단일 이미지에서 깊이를 직접 유추할 수 없기 때문입니다. 대신, 그것을 EKF를 사용하여 비디오 프레임의 체인 이미지 분석을 통해 계산합니다.

## Mobile devices
오늘날에는 Ownership과 스마트폰의 사용이 널리 퍼져 있습니다. 이러한 장치는 일반적으로 후면에 단일 카메라가 있습니다. 이 하드웨어는 monocular SLAM 시스템에 필요한 모든 것이므로 monocular SLAM의 큰 장점은 추가 하드웨어 없이도 휴대폰에서 SLAM을 사용할 수 있다는 것입니다. 이로 인해 SLAM 기술의 액세스가 훨씬 쉬워졌습니다.

## The problem of infinite distance
여러 대의 카메라가 포함된 SLAM시스템에서도 카메라 간 오프셋을 사용하여 멀리 있는 물체의 거리를 직접 추론하는 것은, 불가능하지는 않지만 매우 어렵습니다.
==**이는 카메라 간의 거리가 예상 거리와 비교하여 매우 작기 때문입니다. 따라서 각 카메라의 관찰 이미지에서 물체가 동일한 것처럼 보이게 됩니다. 즉, 거리는 무한한 것으로 보입니다.**==

단일 카메라를 사용하여 SLAM 문제를 해결한다고 해서 동일한 랜드마크를 관찰하는 다른 카메라의 오프셋을 통해 깊이를 추론할 수 있다고 가정하지는 않습니다. ==**서로 다른 시간과 전체 위치(로봇 시스템)에서 캡쳐된 이미지를 비교하여 깊이를 계산하므로, monocular SLAM 알고리즘의 일부를 오프셋 카메라를 사용하여 무한 거리 문제를 해결하는 시스템에서 사용할 수 있습니다.**==

## What about other SLAM techniques?
monocular SLAM을 사용하는데 있어 가장 큰 어려움은 단일 로봇 상태(위치 및 방향)를 사용하여 이미지의 깊이를 직접 추론 할 수 없다는 것입니다. 따라서 로봇으로부터 거리가 떨어진 물체를 유추할 수 없다는 것입니다.
이를 해결 가능한, 직접 추론하는 순수한 monocular 사용 방법 외에 많은 SLAM 기술이 있습니다.
- **Multiple cameras**
-많은 SLAM 방법은 다중 오프셋 카메라를 사용하여 두 눈을 사용하는 사람과 같은 방식으로 가까운 물체의 거리를 직접 추론합니다. 이로 인해 일반적으로 자율 주행차 및 무인 항공기(드론)와 같은 실제 상용 분야에서 더 실용적입니다. 두 대의 시각적 카메라가 포함 된 스테레오 SLAM은 특히 널리 사용되는 기술입니다.
- **Depth sensors**
-Arras와 Tomatis (5)는 전통적인 레이저 거리계와 함께 단일 시각 카메라를 사용하여 이미지의 깊이를 결정합니다. 따라서 로봇 앞의 환경에서 물체와의 거리를 결정한다는 것입니다. 이것은 레이저 신호 전송과 전송 시점과 동일한 시점에서 반사 수신 사이의 시간을 계산하여 작동합니다. 빛의 속도를 고려하여 쉽게 수행 할 수 있습니다.
Xbox 360 및 Xbox One 게임 콘솔을 위해 Microsoft에서 주로 만든 Kinect 센서는 적외선 깊이 센서를 사용합니다. 하드웨어에는 RGB 카메라, 적외선 송신기 및 적외선 수신기가 포함됩니다. 레이저 깊이 센서를 사용하는 것과 같은 방식으로 물체 (예 : 게임 콘솔 사용자)와의 거리를 계산합니다. 이 센서는 모바일 로봇에도 사용됩니다 .
- **Inertia sensors (관성 센서)**
-2012 년에 발표 된 보고서에서 Wang et al. 단일 카메라 외에 관성 센서를 사용하여 로봇의 움직임을 관찰하여 환경에서의 위치에 대한 추정치를 향상시키는 SLAM 알고리즘을 제시합니다. (7)

**- Reference list**

1.Royer E, Lhuillier M, Dhome M, Lavest J-M. Monocular vision for mobile robot localization and autonomous navigation. International Journal of Computer Vision. [Online] 2007;74(3): 237–260. Available from: http://maxime.lhuillier.free.fr/pIjcv07.pdf [Accessed: 31st January 2016]
2.Prisacariu VA, Kähler O, Murray DW, Reid I. Simultaneous 3D tracking and reconstruction on a mobile phone. In: IEEE (ed.) 2013 IEEE International Symposium on Mixed and Augmented Reality. Adelaide, Australia: IEEE; 2013. p. 89–98.
3.Leutenegger S. Group project supervision meeting. 11th February 2016.
4.Lemaire T, Berger C, Jung I-K, Lacroix S. Vision-based SLAM: Stereo and Monocular approaches. International Journal of Computer Vision. [Online] 2007;74(3): 343–364. Available from: http://www.cs.ait.ac.th/~mdailey/cvreadings/Lemaire-SLAM.pdf [Accessed: 4th March 2016]
5.Arras KO, Tomatis N. Improving robustness and precision in mobile robot localization by using laser range finding and monocular vision. [Online] IEEE, 1999 [Accessed: 4th March 2016] p. 177–185. Available from: http://ieeexplore.ieee.org/ielx5/6694/17915/00827638.pdf?tp=&arnumber=827638&isnumber=17915 [Accessed: 4th March 2016]
6.Cong R, Winters R. How Does The Xbox Kinect Work. [Online] Jameco Electronics. Available from: http://www.jameco.com/jameco/workshop/howitworks/xboxkinect.html [Accessed: 13th March 2016]
7.Wang K, Liu Y, Li L. A new algorithm for robot localization using monocular vision and inertia/odometry sensors. [Online] IEEE; p. 735–740. Available from: http://ieeexplore.ieee.org/xpls/abs_all.jsp?arnumber=6491055 [Accessed: 31st January 2016]
8.Bodin B. SLAMBench. [Online] Android Apps on Google play. Available from: https://play.google.com/store/apps/details?id=project.pamela.slambench [Accessed: 10th March 2016]



[Reference Link](https://www.doc.ic.ac.uk/~ab9515/introductiontomonocular.html)
- - -

# 3) What is Visual SLAM Technology and what is it used for?
## Visual SLAM의 정의
**Visual SLAM이란,** ==**"Visual simultaneous localization and mapping"**== 의 약자입니다. 다양한 응용 프로그램을 통해 임베디드 비전에서 중요한 발전을 빠르게 달성했습니다.
상업적으로 말하면, 기술은 아직 초기 단계입니다. 그러나 다른 Vision & Navigation System의 단점을 해결하고 큰 상업적 잠재력과 가치를 갖고 있습니다.
Visual SLAM은 특정 알고리즘이나 소프트웨어를 참조하지 않습니다. 주변 환경과 관련하여 센서의 위치와 방향을 결정하는 동시에, 해당 센서 주변 환경을 Mapping하는 Process를 나타냅니다.
SLAM 기술에는 여러가지 유형이 있으며 일부는 카메라를 전혀 사용하지 않습니다. **==Visual SLAM은 특정 유형의 SLAM System으로, 3D Vision을 활용하여 환경이나 센서 위치를 모를 때 '위치 및 매핑 기능'을 수행합니다.==**
이는 다양한 형태로 제공되지만 전체 개념은 모든 시각적 SLAM 시스템에서 동일한 방식으로 작동합니다. 기본적으로 이 시스템의 목표는 Navigation 목적으로 자신의 위치와 관련하여 주변을 매핑하는 것입니다.

## How Does Visual SLAM Technology Work?
대부분의 시각적 SLAM 시스템은 연속적인 카메라 프레임을 통해 설정 점을 추적하여 3D위치를 삼각 측량하는 동시에 이 정보를 사용하여 카메라 포즈를 추정합니다.
**==다른 형태의 SLAM 기술과 달리 Visual SLAM은 "단일 3D Vision Camera'로 가능합니다.==**
각 프레임을 통해 충분한 수의 지점이 추적되는 한 센서의 방향과 주변 물리적 환경의 구조를 빠르게 이해할 수 있습니다.
**==모든 Visual SLAM 시스템은 일반적으로 '번들 조정'이라는 알고리즘 솔루션을 통해 재투영 오류 또는 투영된 지점과 실제 지점의 차이를 최소화하기 위해 지속적으로 노력하고 있습니다.==** Visual SLAM 시스템은 실시간으로 작동해야하므로, 위치 데이터와 매핑 데이터는 개별적으로 번들 조정을 거치지만, 동시에 병합되기 전에 더 빠른 처리 속도를 제공합니다.

## What Types of Applications Use Visual SLAM?
Visual SLAM은 아직 상용화 단계에 있습니다. 광범위한 환경에서 엄청난 잠재력을 갖고 있지만 여전히 새로운 기술입니다.
**==1. 이는, '증강 현실 응용 프로그램'의 중요한 부분이 될 것입니다.==**
실제 이미지를 가상 세계에 정확하게 투영하려면, 실제 환경을 정확하게 매핑해야만 하고 Visual SLAM 기술만이 이러한 수준의 정확도를 제공할 수 있습니다.
**==2. Visual SLAM 시스템은 다양한 '현장 로봇'에서도 사용됩니다.==**
예를 들어 화성을 탐험하기 위한 로버와 착륙선은 Visual SLAM 시스템을 사용하여 자율적으로 탐색합니다. 드론뿐만 아니라 농업 분야의 현장 로봇도 동일한 기술을 사용하여 작물 분야를 독립적으로 이행할 수 있습니다. 자율 주행 차량은 Visual SLAM 시스템을 사용하여 주변 세계를 매핑하고 이해할 수 있습니다.

**==3. 이 시스템의 주요 잠재적 opportunity 중 하나는 특정 응용 프로그램에서 GPS 추적 및 탐색을 대체할 수 있다는 것입니다.==**
GPS 시스템은 실내 혹은 하늘의 시야가 방해되는 대도시에서는 유용하지 않으며 몇 Meter 이내에서만 정확하다는 치명적인 단점이 있습니다. Visual SLAM 시스템은 위성 정보에 의존하지 않고 주변의 실제 세계를 정확하게 측정하기 때문에, 이러한 문제를 해결할 수 있습니다.

Visual SLAM 기술은 많은 잠재 응용분야들을 가지고 있으며, 기술에 대한 수요는 앞에서 언급한 증강 현실 / 자율 주행 차량 / 기타 제품의 상용화에 큰 도움이 되기 때문에 증가할 것으로 예측됩니다.

사전에 데이터 Point를 몰라도, 카메라의 위치와 주변 환경을 감지하는 기능은 매우 어렵습니다. 그러나 Visual SLAM 시스템은 이러한 과제를 해결하는데 매우 효과적이고 가장 정교한 임베디드 Vision 기술 중 하나로 부상하고 있습니다.

-[Reference Link](https://www.visiononline.org/blog-article.cfm/What-is-Visual-SLAM-Technology-and-What-is-it-Used-For/99)