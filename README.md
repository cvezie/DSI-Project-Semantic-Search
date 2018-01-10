# Semantic Search

## The Task
The objective of this assignment is to engineer a novel wikipedia search engine using what I've learned about data collection, infrastructure, and natural language processing.

The task has **two sections**:
- Data collection
- Search algorithm development

**stretch goals:**
- Predictive modeling

![](http://interactive.blockdiag.com/image?compression=deflate&encoding=base64&src=eJxdjrsOwjAMRXe-wlsmRhaQkDoiMSDxBW5slahtHDmGCiH-nfQxtKy-59zruhPfUsAGPjsA56XvMdIRSIbYCZKD_RncENqQuGBQ3S7TidCwxsynjZUZ1T8m4HqvJlXZnhrBJMHBbWlTDHEeSFravYUXQy_E3TKrwbioMKb5z16UmRxfXZurVY_GjegbhqJIjaXm-wNmzE4W)

### Part 1 -- Collection

#### Goals
- To query the wikipedia API and **collect all of the articles** under the following wikipedia categories:

    * [Machine Learning](https://en.wikipedia.org/wiki/Category:Machine_learning)
    * [Business Software](https://en.wikipedia.org/wiki/Category:Business_software)

- To write raw page text and its category information to a collection on a Mongo server running on a dedicated AWS instance.

- Write code that is modular enough that any valid category from Wikipedia can be queried by my code. 

**Note:** Both "Machine Learning" and "Business Software" contain a heirarchy of nested sub-categories. Make sure to pull every single page within each parent category, not just those directly beneath them. Take time to explore wikipedia's organization structure. 

**stretch goals**  
Make it so that my code can be run via a python script e.g.

```bash
$ docker run --rm -v $(pwd):/home/jovyan jupyter/scipy-notebook python download.py #SOME_CATEGORY#
```
This docker command starts a disposable scipy-notebook container for one-time use to run my script, `download.py`. Where `#SOME_CATEGORY#` is the wikipedia category to be downloaded. Read about passing arguments to python scripts here: https://docs.python.org/3/library/sys.html. 

**stretch goals**  
Make it so that my code can query nested sub-categories e.g.

```bash
$ docker run --rm -v $(pwd):/home/jovyan jupyter/scipy-notebook python download.py #SOME_CATEGORY# #NESTING_LEVEL#
```

### Part 2 -- Search

#### Goals
Use Latent Semantic Analysis to search my pages. Given a search query, find the top 5 related articles to the search query. Start with SVD and cosine similarity. 

**stretch goals**  
Make it so that my code can be run via a python script e.g.

```bash
$ docker run --rm -v $(pwd):/home/jovyan jupyter/scipy-notebook python search.py #SOME_TERM#
```

### Part 3 -- Predictive Model

- Build a predictive model from the data I've just indexed. Specifically, when a new article from wikipedia comes along, be able to predict what category the article should fall into. The goal is a training script of some sort that is runnable and will estimate a model. 

Make it so that my code can be run via a python script e.g.

```bash
$ docker run --rm -v $(pwd):/home/jovyan jupyter/scipy-notebook python train.py
```

Pass the url of a wikipedia page to generate a prediction for the best category of that page, along with a probability of that being the correct category. 

Make it so that my code can be run via a python script e.g.

```bash
$ docker run --rm -v $(pwd):/home/jovyan jupyter/scipy-notebook python predict.py #URL#
```

## Infrastructure

Run a MongDB server on a dedicated t2.micro instance. 
Run my Jupyter environment locally.


