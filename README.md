# End-To-End-DL-Project

## Steps

* create and activate the environment
```bash
conda create -n dl-env python=3.8 -y
conda activate dl-env
```

* create template.py to add folder structure
```bash
touch template.py
```

* define a setup.py file

* add required libraries to requirements.txt and pip install it
```bash
pip freeze
pip freeze | grep pandas
```
**Note:** The **Logging** is a means of tracking events that happen when some software runs. 
*  add code to src/cnnClassifier/__init__.py  to define logging and create test.py for test purpose

**Note:** The **utils.py** makes it easy to execute common tasks in Python scripts
* define utils (src/cnnClassifier/utils/utils.py)

