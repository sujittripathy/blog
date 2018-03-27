---
title: "Managing Jupyter Notebooks on Cloud"
date: 2017-11-24
---



Collaborative coding is one of the key component to build better software. Open source software like [GitHub](https://github.com/about), is a community of 25 million members maintains their code and projects on the cloud.

The question is - How can we manage our Data Science projects on the cloud, so that we can execute anywhere, anytime and can support cloning, sharing etc.. <a href="https://github.com/jupyter/notebook" target="_blank">Jupyter notebook</a> (previously iPython Notebook) is a popular open-source platform for doing Data Science, however for the local development the complete Data Science package including Jupyter can be downloaded from [Anaconda distribution](https://www.anaconda.com/download/#macos), which is local development. Wouldn't it be nice if we can get the entire Jupyter environment setup running in the cloud with all necessary packages installation?

The answer is [Azure Notebook](https://github.com/jupyter/notebook). A Jupyter Notebook on the cloud which supports languages such as ***Python***(both v2 & v3), ***R*** and ***F#***.

Here are few simple steps on how to manage the Notebooks :

## Login to https://azure.notebooks.com**

To manage the Notebook portfolio, need to login to https://azure.notebooks.com. This needs a Hotmail account with existing one or by creating a new one.

## Create a new Library

To manage the notebooks first, a Library is needed which is kind of a folder to hold all the notebooks. Click the +New Library link to create the same and give a unique name.

![](/img/jupyter_on_cloud/img1.png)


The other way a New Library can be created by ***importing from GitHub***. The iPythonNotebooks can be imported from GitHub.

![](/img/jupyter_on_cloud/img2.png)

## Create the Notebook

After Library creation the next step is to create and execute the Notebook.

Click on + New link to add files to Library. Give a name, and select the File type is Python 3.6 Notebook. This is important as the notebook environment will be set by the file type. Note that Azure Notebook supports R & F# though, but here we will go for Python:). The Notebook allows to import from locally saved notebooks (.ipynb files) or imported from GitHub directly from the 'From Computer' or 'From URL' tab. If your notebook exists in GitHub then Notebook can directly import the same.

![](/img/jupyter_on_cloud/img3.png)

## Executing the Notebook in Python

As the Notebook has been created, now it's time to execute the same. To execute, navigate to your Library which you have just created and click on the newly created notebook.

![](/img/jupyter_on_cloud/img4.png)

The notebook starts the Python instance and opens the notebook. Now the notebook is up and running:) The environment comes with all the necessary Data Science packages such as Pandas, Numpy, Matplotlib, Seaborn for charts etc.. so, the notebook can up and running in just a few minutes.

![](/img/jupyter_on_cloud/img5.png)

## Upload and Download Data

None of [Data Science](https://en.wikipedia.org/wiki/Data_science) experiment or projects can happen without Data, which is key the ingredient. The Data can be uploaded in [AWS S3](https://aws.amazon.com/s3/details/) and referred from Notebook however, Notebook supports the Data uploads right from out of the box and the file present in the same folder as the Notebook.

Data files (csv, json etc..) can be uploaded from Data > Upload. The files goes to local home directory.

![](/img/jupyter_on_cloud/img6.png)

The uploaded file can be downloaded from Data > Download location.


If you found this post interesting on how we can manage our entire Notebook and perform the experiment on the cloud, then you may find this interesting to know that Google recently made their internal [Google Colaboratory](https://research.google.com/colaboratory/unregistered.html) as open to the public where access is being provided on a request basis as of today.

