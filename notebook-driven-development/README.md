# Jupyter Notebook Driven Development with PYNT (PYthon iNTeractive)

https://github.com/ebanner/pynt

## The Short Description

In this talk, I will present pynt (*py*thon i*nt*eractive), a tool which leverages the interactive capabilities of Jupyter Notebooks to provide a rich programming environment conducive to the later stages of software development. I will begin by discussing common workflow in software development, as well their limitations. I will then motivate the merits of pynt by demonstrating how adopting a Jupyter-Notebook-Driven-Development workflow can overcome some of these limitations, and then how pynt streamlines this workflow. I will end with a feature-tour of pynt and the different approach to software development workflow that pynt encourages.

## The Long Description

Jupyter Notebooks are a powerful tool in the early stages of software development. Features such as executable code cells allow developers to quickly perform experiments due to the tight feedback loop provided. Markdown cells allow developers to document these experiments in a coherent way with support for rich content such as links, images, and videos. It is this process of on-the-fly editing, evaluation, organization, and visualization that allows developers to rapidly understand how bits of code compose into larger functioning units.

However, once the developer hits a certain point, it is common practice to transfer code into a python module. Reasons for this decision include a desire to decrease duplication and increase organization. At this point in the development process, developers typically ditch Jupyter Notebooks in favor of tools such as text editors and integrated development environments, often transitioning to an edit-compile-run approach, never to return.

The edit-compile-run approach to software development and its drawbacks are a familiar reality to most developers; namely the delay between code modification and the seeing the effect of the change, the effort required to perform context switching during the compile and run phases, and the implicit (rather than explicit) feedback of the effect of the code change during the run step. The end effect is a more arduous development cycle and hence a decreased ability to maintain and sustain complex software systems.

In this talk for intermediate developers, we will review a host of approaches to overcome the limitations of the edit-compile-run approach to software development (e.g. inserting logging, print, and debugging (i.e. pdb) break points; read-eval-print-loops (REPLs); interactive programming environments (e.g. live-py-mode and pry)) as well as their limitations. Attendees will then learn a simple trick to incorporate Jupyter Notebooks into their development workflow which overcomes many of these issues. Finally they will be introduced to a tool called pynt which streamlines such a Jupyter-Notebook-Driven-Development workflow.

The majority of the talk will be centered around pynt. Attendees will learn about the main features of pynt, including including on-the-fly notebook creation, sending and evaluating regions of code to a Jupyter Notebook, auto-scrolling the generated notebook, and capabilities for enabling a debugger-driven-development workflow. This will lead us into a discussion of a view of software development that pynt encourages; namely to have developers spend the majority of time in a jupyter notebook editing, experimenting, and visualizing data through all phases of the software development process.

Attendees will leave the talk with the understanding that Jupyter Notebooks need not be a tool limited to prototyping in the early stages of software development, but can be used to great effect during later stages. They will understand the role that pynt plays in enriching software development via interactivity, thereby overcoming key limitations of the edit-compile-run cycle and other popular interactive programming environments.

## About the Presenter

Edward Banner is a Data Scientist at mosss. Previously Edward was an instructor at GalvanizeU, a Masters of Data Science program. During Edward’s time at GalvanizeU he gave dozens of lectures to students on deep learning and recorded at least as many live-coding videos with an emphasis on Khan Academy-style instruction. More recently, he presented pynt to a group of emacs hackers at the Emacs SF Meetup group.
