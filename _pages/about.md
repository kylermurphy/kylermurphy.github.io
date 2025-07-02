---
permalink: /
title: "About"
excerpt: "About"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

I am an Independent Contractor working in Thunder Bay. I am an expert in statistical analysis and machine learning with a research focus in Space Weather and the dynamics of the magnetosphere during geomagnetic storms and substorms. As a contractor I provide expertise in research and analysis, project management, proposal development, and machine learning. Having worked in academia for over 20 years I have also developed a clear teaching philosophy that focuses on engaging students and developing vital soft and critical thinking skills.

## Recent Work

**Research:** My new paper [Understanding and Modeling the Dynamics of Storm-Time Atmospheric Neutral Density Using Random Forests][1] highlights the importance of geomagnetic storms in the dynamics of atmospheric neutral density. The paper also provides a new machine learning model for predicting atmospheric neutral density using random forests. The new machine learning model can be found on [GitHub][2] and [Zenodo][3]. An [example Jupyter notebook][4] walks users through how derive model predictions  

**Communication and Service:** The [Magnetosphere Online Seminar Series][5] was established in response to the cancelation of several scientific meetings and to encourage continued interaction within the Space Physics community during the Covid-19 pandemic. The series hosts seminars on Zoom and YouTube live streams and watch previous seminars on the [YouTube channel][6].

**Projects:** [GMAG][7] is a Python module providing the utility to download and load data from various ground-based magnetometer arrays in a Pandas DataFrame. The [GMAG site][8] provides an overview of the module, a few examples, details for each [Array supported by the module][9], a [map][10] of magnetometer stations, and a [searchable table of the geographic and geomagnetic coordinates][11] of magnetometer stations in each array.

The most recent update of GMAG introduces a new module for deriving ground-based induced electric fields from magnetometer measurements. The the ```efield``` module provides routines to calculate the 1-D surface impedence and subsequently the induced electric field. Resistivity profiles for select stations are also provided along with a simple routine to read in these profiles. Additional profiles will be added soon.



[1]:https://doi.org/10.1029/2024SW003928
[2]:https://github.com/kylermurphy/mltdm
[3]:https://doi.org/10.5281/zenodo.15091438
[4]:https://github.com/kylermurphy/mltdm/blob/main/Notebooks/RF_predict.ipynb
[5]:https://msolss.github.io/MagSeminars/
[6]:https://www.youtube.com/channel/UCNlOK9mCmI3V111EHQRCuEQ?view_as=subscriber
[7]:https://github.com/kylermurphy/gmag
[8]:https://kylermurphy.github.io/gmag/
[9]:https://kylermurphy.github.io/gmag/arrays
[10]:https://kylermurphy.github.io/gmag/stations
[11]:https://kylermurphy.github.io/gmag/cgm_2000.html
