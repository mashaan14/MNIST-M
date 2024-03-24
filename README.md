# MNIST-M Dataset
MNIST-M is created by blending digits from the original set (MNIST) over patches that are randomly extracted from color photos in [BSDS500](https://www2.eecs.berkeley.edu/Research/Projects/CS/vision/grouping/resources.html) (Arbelaez et al., 2011). MNIST-M is usually used as a target dataset in domain adaptation tasks (Ganin et al., 2016).

<p align="center">
  <img width="1200" src="sample.png">
</p>

## MNIST-M for `torchvision`
The file `MNIST-M.zip` contains images from MNIST-M dataset organized in subfolders, where each folder represents a class. This setup makes it ready to be imported using `torchvision.datasets.ImageFolder`.

## Making MNIST-M `torchvision` ready
You might have donwloaded MNIST-M, where images are not organized into subfolders. In this case, this code fragment could be useful. Run it twice, one for `mnist_m_train_labels.txt` and another run for `mnist_m_test_labels.txt`

```python
import os
import shutil
import pandas as pd

df = pd.read_csv('mnist_m_train_labels.txt', sep=" ", header=None)
df.columns = ["file name", "subfolder"]
cwd = os.getcwd().replace('\\', '/')

for index, row in df.iterrows():
  print(row['file name'], row['subfolder'])
  shutil.move(os.path.join(cwd+'/',row['file name']), 
              os.path.join(cwd+'/', str(row['subfolder'])))
```
