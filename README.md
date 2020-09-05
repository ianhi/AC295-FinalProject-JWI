Authors: Jenny Huang, Ian Hunt-Isaak, William Palmer
# Write up
This was our final project for  https://harvard-iacs.github.io/2020-AC295/. We wrote a medium article about this! Check it out here: https://medium.com/institute-for-applied-computational-science/how-we-built-an-easy-to-use-image-segmentation-tool-with-transfer-learning-546efb6ae98

## Image segmentation code is now availiable on PyPi!
The image segmenter in this project is now availiable on pypi via [mpl-interactions](https://github.com/ianhi/mpl-interactions), see documentation [here](https://mpl-interactions.readthedocs.io/en/latest/examples/image-segmentation.html). Also this project inspired [ipysegment](https://github.com/ianhi/ipysegment), an HTML5 canvas based canvas based image segmenter for use in jupyter notebooks. ipysegment will be significantly less laggy to use, but currently has fewer features.

# Trying it out


**docker**

From Dockerhub:
```
sudo docker run -p 8888:8888 -e JUPYTER_ENABLE_LAB=yes ianhuntisaak/ac295-final-project:v3
```

**Binder**  
We don't recommend this, everything will be very slow (also it currently fails to build 😢): [![Binder](https://mybinder.org/badge_logo.svg)](https://gesis.mybinder.org/binder/v2/gh/ianhi/AC295-final-project-JWI/master?urlpath=lab) 



# Installing dependencies

Or you could install it locally. We have a conda environment file in the binder directory. So you can make an environment with the following commands:

```bash
conda create -n segmentation -f binder/environment.yml -y && conda activate segmentation
jupyter labextension install @jupyter-widgets/jupyterlab-manager --no-build
jupyter labextension install @jupyter-widgets/jupyterlab-sidecar jupyter-matplotlib
```
## Import structure
There are separate directories for notebooks and python files because otherwise things become a real mess. To import something from a python file in the lib directory put the following at the top of your python notebook:
```python
# set up path for relative imports
import os
import sys
module_path = os.path.abspath(os.path.join('../'))
if module_path not in sys.path:
    sys.path.append(module_path)
```

Then you can do `from lib.____ import ____`


# Updating docker image

Follow: https://ropenscilabs.github.io/r-docker-tutorial/04-Dockerhub.html


**build**
```bash
sudo docker build -t ianhuntisaak/ac295-final-project:<tag> .
```

**Verify that it works**
If you use a port other than 8888, e.g. `-p 8889:8888` then you need to change the port in the URL printed in the terminal, can't just copy paste.
```bash
sudo docker run -p 8888:8888 -e JUPYTER_ENABLE_LAB=yes ianhuntisaak/ac295-final-project:<tag>
```

**push to dockerhub**
```bash
sudo docker push ianhuntisaak/ac295-final-project
```

**update the tag version in this readme**
Turns out using the `latest` tag is a bit of a nightmare: https://medium.com/@mccode/the-misunderstood-docker-tag-latest-af3babfd6375
