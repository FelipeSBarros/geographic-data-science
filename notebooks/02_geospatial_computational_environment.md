---
jupyter:
  jupytext:
    formats: ipynb,md
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.3'
      jupytext_version: 1.10.3
  kernelspec:
    display_name: Python 3
    language: python
    name: python3
---

```python tags=["remove-cell"]
import warnings
warnings.filterwarnings("ignore")
```

# Geospatial Computational Environment
## Computational Tools for Geographic Data Science

```python tags=["remove-cell"]
from IPython.display import Image
```

This chapter provides an overview of the scientific and computational context
in which the book is framed. Many of the ideas discussed here apply beyond Geographic
Data Science but, since they have been a fundamental pillar in shaping the
character of the book, we consider them worth discussing. First, we will explore debates around Open
Science, its origins, and how the computational community is responding.
In particular, we will discuss computational notebooks, open-source
packages, and reproducible platforms. Having covered the conceptual
background, we will turn to a practical introduction of the key infrastructure
this book relies on: Jupyter Notebooks and JupyterLab, Python packages,
and a containerized platform to run the book.


## Open Science

The term Open Science has grown in popularity in recent years. Although it is
used in a variety of contexts with slightly different meanings {cite}`cruwell2019seven`, a general
sense of the intuition behind Open Science is the understanding that the
scientific process, at its core, is meant to be transparent and accessible.
In this context, the focus on openness is not to be seen as an "add-on" that
changes the general approach only cosmetically, but as a key component of what
makes science Science. Indeed the scientific process, understood as one where
we "build on the shoulders of Giants" and progress through dialectic, can only
work properly is there is enough transparency and accessibility that the
community can access and study both results _and_ the process that created
them.

To better understand the argument behind modern Open Science, it is useful
to take a historical perspective. The idea of openness was ingrained at the
core of early scientists. In fact that was one of the key differentials with
their contemporary "alchemists" which, in many respects, were working on
similar topics albeit in a much more opaque way {cite}`Nielsen_2020`. Scientists
would record the field or lab experiments on paper notebooks or diaries,
providing enough detail to, first, remember what they had done and how they
had arrived at their results; but also to ensure other members of the
scientific community could study, understand, and replicate their findings.
One of the most famous of these annotations are Galileo's drawings of Jupiter ([source](https://commons.wikimedia.org/wiki/File:Medicean_Stars.png)) and the Medicean stars:

```python caption="Galileo's drawings of Jupyter and the Medician stars, showing the power of diagrams inside of scientific texts." tags=["remove-input"]
url = ("https://upload.wikimedia.org/wikipedia/"\
       "commons/c/ca/Medicean_Stars.png")
Image(url, width=250)
```

There is a growing perception that much of the original ethos of Science to
operate through transparency and accessibility has been lost. A series of
recent big profile scandals have even prompted some to call it a state of
crisis {cite}`Ioannidis_2007`. This "crisis" arises because the analyses 
that scientists conduct are difficult to repeat, or even understand in 
detail the steps that were taken to arrive at results.

Why is there a sense that Science is no longer open and
transparent in the way Galileo's diaries were? Although certainly not the only
or even the most important one, technology plays a role. The process and workflow
of original scientists relied on a set of analog technologies for which an
analog parallel set of tools was developed to keep track and document
progress. Hence the paper notebooks where biologists drew species, or chemists
painstakingly detailed each step they took in the lab. In the case of social
sciences, this was probably easier in the sense that quantitative data was not
abundant and much of the analysis relied either on math or small datasets
which could be directly documented in the original publications.

However Science has evolved a great deal since then, and much of the
experimental workflow is dominated by a variety of machinery, most
prominently by computers. Most of the Science done today, at some
point in the process, takes the form of operations mediated through software
programs. In this context, the traditional approach of writing down in a paper
notebook every step followed becomes dislocated from the medium in which most of
the scientific work takes place.

The current state of Science in terms of transparency and openness is prompting
for action {cite}`Rey_2009`. On the back of these debates, the term
"reproducibility" is also gaining traction. Again, this is a rather general
term but, in one variant or another, its definition alludes to the need of
scientific results to be accompanied by enough information and detail so they
could be repeated by a third party. Since much of modern science is mediated
through computers, reproducibility thus poses important challenges for the
computational tools and practices the scientific community builds and relies on. Although
there is a variety of approaches, in this book we focus on what we see as the
emerging consensus. This framework enables to record and express entire
workflows in a way that is both transparent and that fosters efficiency and
collaboration.

We structure our approach to reproducibility in three main layers that build on
each other. At the top of this "stack" are _computational notebooks_; supporting
the code written in notebooks are _open source packages_; and making possible to
transfer computations across different hardware devices and/or architectures
are what we term _reproducible platforms_. Let us delve into each of them with
a bit more detail before we practically show how this book is built on this
infrastructure (and how you too can reproduce it at home!).

### Computational notebooks

Computational notebooks are the twenty-first Century sibling of Galileo's notebooks.
Like their predecessors, they allow researchers, (data) scientists, and
computational practitioners to record their practices and steps taken as they
are going about their work; unlike the pen and paper approach, computational
notebooks are fully integrated in the technological paradigm in which research
takes place today. For these reasons, they are rapidly becoming the
modern-day version of the traditional academic paper, the main vehicle on
which (computational) knowledge is created, shared, and consumed.
Computational notebooks (or notebooks, from now on) are spreading their
reach into industry practices, being used, for example, in reports. Although,
they were designed within a broader scope of application, computational notebooks
have several advantages for Geographic Data Science work {cite}`boeingAB2020`.

All implementations of notebooks share a series of 
core features. First, a notebook comprises a single file that stores narrative text,
computer code, and the output produced by code. Storing both
narrative and computational work in a _single file_ means that the entire
workflow can be recorded and documented in the same place, without having to 
resort to ancillary devices (like a paper notebook). A second feature of
notebooks is that they allow _interactive work_. Modern computational work
benefits from the ability to try, fail, tinker, and iterate quickly until a
working solution is found. Notebooks embody this quality and enable the user
to work interactively. Whether the computation takes place on a laptop or
on a data center, notebooks provide the same interface for interactive
computing, lowering the cognitive load require to scale up. Third, notebooks
have _interoperability_ built in. The notebook format is designed for
recording and sharing computational work, but not necessarily for other stages
of the research cycle. To widen the range of possibilities and
applications, notebooks are designed to be easily convertible into other
formats. For example, while a specific application is required to open and edit
most notebook file formats, no additional software is required to convert them
into PDF files that can be read, printed, and annotated without the need of technical
software.

Notebooks represent the top layer on the reproducibility stack. They can capture
in detailed and reproducible ways work that is specific about a given project: 
what data is used, how it is read, cleaned, and transformed; what algorithms are used, how they
are combined; how each figure in the project is generated, etc. Guidance on how
to write notebooks in efficient ways is also emerging (e.g. {cite}`Rule_2019`).

### Open source packages

To make notebooks an efficient medium to communicate computational work, it is
important that they are concise and streamlined. One way to achieve this goal is
to only include the parts of the work that are unique to the application being
recorded in the notebook, and to avoid duplication. From this it follows that
if a piece of code is used several times across the notebook, or even across
several notebooks, that functionality should probably be taken out of the
notebook and into a centralized place where it can be accessed whenever
needed. In other words, such functionality should be turned into a package.

Packages are modular, flexible and reusable compilations of code. Unlike
notebooks, they do not capture specific applications but abstractions of
functionality that can be used in a variety of contexts. Their function is to
avoid duplication "downstream" by encapsulating functionality in a way that
can be accessed and used in a variety of contexts without having to re-write
code every time it is needed. In doing so, packages (or libraries, an
interchangeable term in this context) embody the famous hacker motto of D.R.Y.:
"don't repeat yourself".

Open source packages are packages whose code is available to inspect, modify
and redistribute. They fulfill the same functions as any package in terms of
modularizing code, but they also enable transparency as any user can
access the exposed functionality _and_ the underlying code that
generates it. For this reason, for code packages to serve Open Science and
reproducibility, they need to be open source.

### Reproducible platforms

For computational work to be fully reproducible and open, it needs to be
possible to replicate it in a different (computational) environment than where it
was originally created. This means that it is not sufficient to specify in a
notebook the code that creates the final outputs, and to rely on open source
packages for more general functionality; the environment specified by those
two components needs to be reproducible too. This statement, which might seem
obvious and straightforward, is not always so due to the scale and complexity
of modern computational workflows and infrastructures. The old saying "if
it works on my laptop, what's the problem?" is not enough any more, it needs
to work on "any laptop" (or computer).

Reproducible platforms encompass the more general aspects
that enable open source packages and notebooks to be reproducible. A
reproducible platform thus specifies the infrastructure required to ensure a
notebook that uses certain open source packages can be successfully executed.
Infrastructure, in this context, relates to lower-level aspects of the
software stack, such as the operating system, and even some hardware
requirements, such as the use of specific chips such as graphics processing
units (GPU). Additionally, a reproducible platform will also specify the
versions of packages that are required to recreate the results presented in a
notebook.

Unlike open source packages, the notion of reproducible platforms is not as
widespread and generally agreed upon. Its necessity has only become apparent more
recently, and work on providing them in standardized ways is less developed
than in the case of notebook technology or code packaging and distribution.
Nevertheless, some inroads are being made. One area which has experienced
significant progress in recent years and holds great promise in this context is
container technology. Containers are a lightweight version of a virtual
machine, which is a program that enables an entire operating system to run
compartmentalized on top of another operating system. Containers allow to
encapsulate an entire environment (or platform) in a format that is easy to
transfer and reproduce in a variety of computational contexts. The most
popular technology for containers nowadays is Docker, and the opportunities
that it provides to build transparent and transferrable infrastructure for
data science are starting to be explored {cite}`Cook_2017`.

## The (computational) building blocks of this book

### Jupyter Notebooks and JupyterLab

#### Notebooks and cells

This book uses notebooks as the main format in which its content is created.
Each chapter is written as a separate notebook and can
be run interactively. At the same time, we collect all chapters and convert
them into different formats for "static consumption" (i.e.. read only), either
in HTML format for the web, or PDF to be printed in a physical copy.
This section will present the specific format of notebooks we use, and
illustrate its building blocks in a way that allows you to then follow the
rest of the book interactively.

Our choice of notebook is Jupyter {cite}`Kluyver2016jupyter`. A Jupyter notebook is a plain
text file with the `.ipynb` extension, which means that it is an easy file to
move around, sync, and track over time. Internally, it is structured as a plain-text document containing
JavaScript Object Notation that records the state of the notebook, so they 
also integrate well with a host of modern web technologies.
The atomic element that makes up a notebook is called a _cell_. Cells are 
consistent chunks of content that contain either text or code. In fact, a
notebook can be thought of as an ordered collection of cells. Cells can be of
two types: _text_ and _code_.

Text cells contain text written in the Markdown markup language. Markdown is a
popular set of rules to create rich content (e.g. headers, lists, links) from
flat, plain text files without being as complex and sophisticated as other
typesetting approaches. The notebook will then render markdown
automatically. For more demanding or specific tasks, text cells can further 
integrate $\LaTeX$ notation. This means we can write most forms of narrative
relying on markdown, which is more straightforward, and use $\LaTeX$ for
more sophisticated parts, such as equations. Covering Markdown rules in detail
is beyond the scope of this chapter, but the interested reader can inspect the
official GitHub specification of the so-called GitHub-Flavored markdown
{cite}`ghfmd`, the one adopted by the notebook.

Code cells are boxes that contain snippets of computer code. In the case of this
book, all code will be Python, but Jupyter notebooks are flexible enough to
work with other languages.[^kernel_list] Code cells look as follows:

[^kernel_list]: A full list of supported kernels for Jupyter is available at [`https://github.com/jupyter/jupyter/wiki/Jupyter-kernels`](https://github.com/jupyter/jupyter/wiki/Jupyter-kernels)

```python attributes={"classes": [], "id": "", "n": "1"}
# This is a code cell
```

A code cell can be run to execute the code it contains. If such code produces
an output (e.g. a table or a figure), this will be printed as a cell output.
Every time a cell is run, its counter on the notebook interface will go up by one.

#### Rich Content

Code cells in a notebook also enable the embedding of rich (web) content. The
`IPython` package provides methods to access as series of media and bring them
directly to the notebook environment. Let us see how this can be done
practically. To be able to demonstrate it, we will need to _import_ the
`display` module (skip to the next section if you want to learn more about
importing packages):

```python attributes={"classes": [], "id": "", "n": "3"}
import IPython.display as display
```

This makes available additional functionality that allows us to embed rich
content. For example, we can include a YouTube clip by passing the video ID:

```python caption="Embedding rich media in a notebook." tags=[]
display.YouTubeVideo('iinQDhsdE9s')
```

Or we can pass standard HTML code:

```python attributes={"classes": [], "id": "", "n": "5"}
display.HTML(
    """<table>
<tr>
<th>Header 1</th>
<th>Header 2</th>
</tr>
<tr>
<td>row 1, cell 1</td>
<td>row 1, cell 2</td>
</tr>
<tr>
<td>row 2, cell 1</td>
<td>row 2, cell 2</td>
</tr>
</table>"""
)
```

Note that this opens the door for including a large number of elements from the
web, since an `iframe` of any other website can also be included. Of more relevance
for this book, for example, this is one way we can embed interactive maps with an `iframe`:

```python attributes={"classes": [], "id": "", "n": "6"}
osm = """
<iframe width="425" 
        height="350" 
        frameborder="0" 
        scrolling="no" 
        marginheight="0" 
        marginwidth="0" 
        src="http://www.openstreetmap.org/export/embed.html?bbox=-2.9662737250328064%2C53.400500637844594%2C-2.964626848697662%2C53.402550738394034&amp;layer=mapnik" 
        style="border: 1px solid black">
</iframe>
<br/>
<small>
    <a href="http://www.openstreetmap.org/#map=19/53.40153/-2.96545">View Larger Map</a>
</small>
"""
display.HTML(osm)
```

Finally, using a similar approach, we can also load and display local 
images, which we will so throughout the book. For that, we use the `Image`
method:

```python caption="This book's logo, built from Stamen Toner map tiles and from code."
path = "../infrastructure/logo/logo_transparent-bg.png"
display.Image(path, width=250)
```

#### Jupyter Lab

Our recommended way to interact with Jupyter notebooks is through Jupyter Lab.
Jupyter Lab is an interface to the Jupyter ecosystem that brings together
several tools for data science into a consistent interface that enables the user
to accomplish most of her workflows. It is built as a web app following a
client-server architecture. This means the computation is decoupled from the
interface. This decoupling allows each to be hosted in the most convenient and
efficient solution. For example, you might be following this book
interactively in your laptop. In this case, it is likely both the server that
runs all the Python computations you specify in code cells (what we call the
_kernel_) is running locally, and you are interacting with it through your
browser of preference. But the same technology could power a situation where
your kernel is running in a cloud data center, and you interact with Jupyter
Lab from a tablet.

Jupyter Lab' interface has three main areas: [^jlab]

[^jlab]: Depending on the version of JupyterLab you are using, the layout and appearance
may slightly change.

```python caption="An annotated view of the Jupyterlab interface " tags=["remove-input"]
path = "../figures/jupyter_lab.png"
display.Image(path, width=500)
```

At the top we find a menu bar (red box in the figure) that allows us to open,
create and interact with files, as well as to modify the appearance and 
behavior of Jupyter Lab. The largest real estate is occupied by the main
pane (blue box). By default, there is an option to create a new notebook, open
a console, a terminal session, a (markdown) text file, and a window for
contextual help. Jupyter Lab provides a flexible workspace in that the user
can open as many windows as needed and rearrange them as desired by dragging
and dropping. Finally, on the left of the main pane we find the side pane
(green box),
which has several tabs that toggle on and off different auxiliary information.
By default, we find a file browser based on the folder from where the session
has been launched. But we can also switch to a pane that lists all the
currently open kernels and terminal sessions, a list of all the commands in the
menu (the command _palette_), and a list of all the open windows inside the
lab.

### Python and Open Source Packages

#### Python

The main component of this book relies on the Python programming language. Python is a high-
level programming language used widely in (data) science. From satellites controlled by NASA[^nasa]
to courses in economics by Nobel Prize-winning professors, Python is a fundamental component of
modern day science.[^quantecon] 
This book uses Python because it is a good language for beginners and 
high-performance science alike. For this reason, it has emerged as one of the main
and most solid options for Data Science {cite}`te_python`. Python is widely used for data 
processing and analysis both in academia and in industry. There is a vibrant and 
growing scientific community (through the Scientific Python 
library `scipy` and the PyData organization), working in
both universities and companies, to support and enhance the Python's capabilities.
New methods and usability improvements of existing packages (also known as libraries)
are continuously being released. Within the geographic domain, Python is also very widely
adopted: it is the language used for scripting in both the main proprietary enterprise
geographic information system, ArcGIS, 
and the leading open geographic information system, QGIS. All
of this means that, whether you are thinking of Higher Education
or industry, Python will be an important asset, valuable to
employers and scientists alike. 

[^nasa]: For more details, see [`https://www.python.org/about/success/usa/`](https://www.python.org/about/success/usa/)
[^quantecon]: For more details, see [`https://lectures.quantecon.org`](https://lectures.quantecon.org)

Python code is "dynamically interpreted", which means it is run on-the-fly without 
needing to be compiled. This is in contrast to other kinds of programming
languages, which require an additional non-interactive step where a program is 
converted into a binary file, which can then be run. With Python, one does
not need to worry about this non-interactive compilation step. Instead, we can 
simply write code, run it, fix any issues directly, and re-run the code in a
rapid iteration cycle. This makes Python a very productive tool for science, since you can
prototype code quickly. 


#### Open Source Packages

The standard Python language includes some data structures (such as lists and
dictionaries) and allows many basic mathematical operations (e.g. sums, differences,
products). For example, right out of the box, and without any further
action needed, you can use Python as a calculator:

```python attributes={"classes": [], "id": "", "n": "9"}
3 + 5
```

```python attributes={"classes": [], "id": "", "n": "10"}
2 / 3
```

```python attributes={"classes": [], "id": "", "n": "11"}
(3 + 5) * 2 / 3
```

However, the strength of Python as a data analysis tool comes from additional
packages, software that adds functionality to the language itself.
In this book, we will introduce and use many of the core libraries of the 
Python ecosystem for (geographic) data science,
a set of widely-used libraries that make Python fully-featured.
We will discuss each package as we use them throughout the chapters. 
Here, we will show how an installed package can be
loaded into a session so its functionality can be accessed. Package loading
in Python is called _importing_. We will use the library `geopandas` as
an example. The simplest way to import a library is by typing the following:

```python attributes={"classes": [], "id": "", "n": "12"}
import geopandas
```

We now have access to the entire library of methods and classes within the session, which we
can call by prepending `geopandas.` to the name of the function we want.
Sometimes, however, we will want to shorten the name to save keystrokes. This
approach, called _aliasing_, can be done as follows:

```python attributes={"classes": [], "id": "", "n": "12"}
import geopandas as gpd
```

Now, every time we want to access a function from `geopandas`, all we need to
type before the function's name is `gpd.`. However sometimes we rather import
only parts of a library. For example, we might only want to use one function.
In this case, it might be cleaner and more efficient to bring the function
itself only:

```python attributes={"classes": [], "id": "", "n": "12"}
from geopandas import read_file
```

which allows us to use `read_file` directly in the current session. 

Our approach in this
book is to _not_ alias to make our code more readable (`geopandas` instead of `gpd`).
We will be introducing a new library within the text of the first chapter where it is
required so that code is threaded pedagogically with narrative. Once a package has been
introduced, if subsequent chapters rely on it, we will import it at the beginning of the
chapter with all the other, already introduced libraries.

#### Contextual help

A very handy feature of Python is the ability to access on-the-spot help for functions. 
This means that you can check what a function is supposed to do, or how to use it
from directly inside your Python session. Of course, this
also works handsomely inside a notebook, too. There are a couple of ways to access
the help. Take the `read_file` function we have imported above. One way to check its help
dialog from within the notebook is to add a question mark after it:

```python attributes={"classes": [], "id": "", "n": "20"}
read_file?
```

As you can see, this brings up a sub-window in the browser with all the
information you need. Additionally, Jupyter Lab offers the "Contextual Help"
box in the initial launcher. If you open it, the help of every function where
your cursor lands will be dynamically displayed in the contextual help.

If, for whatever reason, you needed to print that information
into the notebook itself, you can use the following `help` function instead:

```python attributes={"classes": [], "id": "", "n": "21"}
help(geopandas.read_file)
```

### Containerized platform

As mentioned earlier in this chapter, 
reproducible platforms encompass technology and practices that help 
reproduce a set of analyses or computational work in a different environment
than that in which it was produced. There are several approaches to implement
this concept in a practical setting. For this book, we use a piece of software called
Docker. Docker is based on a feature of Linux called containers,
which allows to create environments and run processes within them in a way that is
isolated from the host operating system. We decided to settle on Docker mainly for
three main reasons: first, it is widely adopted as an industry standard (e.g.
almost any website today runs on Docker containers), which means it is well
supported and is not likely to disappear any time soon; second, it has also
become a standard in the world of data science, which means foundational
projects such as Jupyter create official containers for these packages; and
third, because of the two previous reasons, developing the book
on top of Docker allows us to easily integrate it with
cloud services or local (clusters of) servers, widening the set of delivery
channels through which we can make the book available to broader audiences.

With Docker, we can create a "container" that includes all the tools required
to access the content of the book interactively. But, what exactly is a 
container? There are several ways to describe it, from very technical
to more intuitive ones. In this context, we will focus on a general
understanding rather than on the technical details behind its magic. One can
think of a container as, well, a "box" that includes
_everything_ that is required to run a certain piece of software. This box can
be moved around, from machine to machine, and the computations it
executes will remain exactly the same. In fact, the content inside the box
remains exactly the same, bit by bit. When we download a container into a
computer, be it a laptop or a data center, we are not performing an install of
the software it contains from the usual channels, for the platform on which we
are going to run it on. Instead, we are downloading the software in the form
that was installed when the container was originally built and packaged,
and for the operating system that was also packaged originally. This is the real
advantage: build once, run everywhere. For the experienced reader,
this might sound very much like their older sibling: virtual machines. Although
there are similarities between both technologies, containers are more 
lightweight and can be run much more swiftly than virtual machines.
The isolated content inside a container interacts with the rest of the computer through
several links that connect the two. For this book, since JupyterLab
is a client-server application, the server runs inside the container and we
access it through two main "doors": one, through the browser, we will
access the main Lab interface; and two, we will "mount" a folder inside the
container so we can use software inside the container to edit files that are
stored outside in the host machine.

"Containers sound great but, how can I install and run one?", you might be
asking yourself at this point. First, you will need to install Docker on your
machine. This assumes you have administrative rights (i.e. you can install
software). If that is the case, you can go to the Docker website[^docker] 
and install the version that suits your operating system. Note that, although container
technology is Linux-based, Docker provides tools to run it smoothly in macOS
and Windows. An install guide for Docker is beyond the scope of this chapter,
but there is much documentation available on the web to this end. We
personally recommend the official documentation,[^docker_docs] but you might find other
resources that suit your needs better.

[^docker]: [`https://www.docker.com/`](https://www.docker.com/)
[^docker_docs]: [`https://docs.docker.com/`](https://docs.docker.com/)

#### Running the book in a container

Once you have Docker up and running on your computer, you can download the
container we rely on for the book. We have written the book using the `gds_env`
project[^gds_env], and that is what we recommend. The `gds_env` provides a
containerised platform for geographic data science. It relies on the official
Jupyter Docker release and builds on top of it a large set of libraries and add-on's
that make the life of the geographic data scientist easier. A new version of
the container including the most recent versions of libraries is released twice a
year. We have written the book using version `6.1`, but it is likely later versions
will work as well.

Downloading the container is akin to installing the
software you need to interact with the book, so you will only need to run it once.
However, keep in mind that the image is relatively large (around 4GB), so you
will need the space on your machine as well as a good internet connection. If
you check those two boxes, you are ready to go. Here are the steps to take:

[^gds_env]: [`https://darribas.org/gds_env`](https://darribas.org/gds_env)

1. Open a terminal or shell. How to do this will depend on your operating
   system:

   - `Windows`: we recommend PowerShell or the Terminal app. Type "PowerShell"
     or "Terminal" on the startup menu
     and, when it comes up, hit enter. This will open a terminal for you.
   - `macOS`: use the `Teminal.app`. You can find it on the Applications
     folder, within the Utilities subfolder.
   - `Linux`: if you are running Linux, you probably already have a terminal
     application of preference. Almost any Linux distribution comes with a
     terminal app built in.

2. Download, or "pull", the GDS container. For this run on the terminal the
   following command:

   ```shell
   docker pull darribas/gds_py:6.1
   ```

That's it! Once the command above completes, you have all the software you
need to interact with this book.

You can now run the container with the following command:

```shell
docker run \
        --rm \
        -ti \
        -p 8888:8888 \
        -v ${PWD}:/home/jovyan/work \
        darribas/gds_py:6.1
```

Let's unpack the command so we understand everything that is going on here to
get further insight into how the container works:

- `docker run`: Docker does a lot of things, to communicate that we want to
  _run_ a new container, we need specify it.
- `--rm`: this flag will ensure the container is removed when you close
  it. This in turn makes sure every time you run it again, you start
  afresh with the exact same set up.
- `-ti`: this flag further ensures that the container is not run in the
  background but in an interactive mode.
- `-p 8888:8888`: with this, we ensure we forward the _port_ from inside
  the container out to the host machine (e.g. your laptop). This flag is
  important because it allows the Jupyter server running inside the container
  to communicate with the browser so we can render the app and send commands.
  It is one of the two doors we discuss above connecting the container with 
  the computer it runs on.
- `-v ${PWD}:/home/jovyan/work`: this is the second door. This flag "mounts" the folder
  from where the command is being run in the terminal (`${PWD}` is the `W`orking 
  `D`irectory) into the
  container so it is visible and editable from inside the container. Such
  folder will be available at the container's `work` folder.
- `darribas/gds_py:6.1`: this specifies which container we want to run. In this
  example, we run the `6.1` version of the `gds_py` container. Depending on when
  you read this, there might be a more recent version that you can try.

The command above will generate output that will look, more or less, like the
following:

```
Executing the command: jupyter notebook
[I 14:45:34.681 NotebookApp] Writing notebook server cookie secret to /home/jovyan/.local/share/jupyter/runtime/notebook_cookie_secret
[I 14:45:36.504 NotebookApp] Loading IPython parallel extension
[I 14:45:36.730 NotebookApp] JupyterLab extension loaded from /opt/conda/lib/python3.7/site-packages/jupyterlab
[I 14:45:36.731 NotebookApp] JupyterLab application directory is /opt/conda/share/jupyter/lab
[I 14:45:36.738 NotebookApp] [Jupytext Server Extension] NotebookApp.contents_manager_class is (a subclass of) jupytext.TextFileContentsManager already - OK
[I 14:45:37.718 NotebookApp] Serving notebooks from local directory: /home/jovyan
[I 14:45:37.718 NotebookApp] The Jupyter Notebook is running at:
[I 14:45:37.719 NotebookApp] http://0fb71d146102:8888/?token=ae7e8017f3e97658a218ec2c2d1fbcc894f09d80f6b5f79c
[I 14:45:37.719 NotebookApp]  or http://127.0.0.1:8888/?token=ae7e8017f3e97658a218ec2c2d1fbcc894f09d80f6b5f79c
[I 14:45:37.719 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
[C 14:45:37.725 NotebookApp] 
    
    To access the notebook, open this file in a browser:
        file:///home/jovyan/.local/share/jupyter/runtime/nbserver-6-open.html
    Or copy and paste one of these URLs:
        http://0fb71d146102:8888/?token=ae7e8017f3e97658a218ec2c2d1fbcc894f09d80f6b5f79c
     or http://127.0.0.1:8888/?token=ae7e8017f3e97658a218ec2c2d1fbcc894f09d80f6b5f79c
```


With this, you can then head to your browser of preference (ideally Mozilla
Firefox or Google Chrome) and point it to `localhost:8888`. This should render
a landing page that looks approximately like this one:

```python caption="The authentification screen for Jupyter notebooks" tags=["remove-input"]
path = ("../figures/jupyter_landing_page.png")
display.Image(path, width=500)
```

To access the lab, copy the token from the terminal (in the example above,
that would be `ae7e8017f3e97658a218ec2c2d1fbcc894f09d80f6b5f79c`), enter it on
the box and click on "Log in". Now you are in!

