# Internal Resources (PIE LAB){#internal}

## Talapas

#### Overview

Talapas is the high performance computing cluster managed by Research Advanced Computing Services (aka RACS) at the University of Oregon. Since it is possible (and maybe even best) to get started with Talapas without knowing too much about the capabilities of the system, we will simply point to the [main website](https://hpcf.uoregon.edu/content/talapas) and the [Talapas Knowledge Base](https://hpcrcf.atlassian.net/wiki/spaces/TCP/overview) for learning more.

In this document, the numbered sections below will deal with separate tasks that users in the lab might want to perform on Talapas. If you learn how to do something that is not documented below, please add it to the list, even if you are unsure that others will find it useful. Or, just point to the documentation available online.

#### Requesting Access

Go to this [website](https://hpcrcf.atlassian.net/servicedesk/customer/portal/1) to request access to the PIE lab Talapas account. Fill out the New Account Request Form, including **pielab** as the PIRG.

#### Using Open OnDemand Interactive Access

The RACS team recommends using an incognito tab in Chrome or Firefox before logging in to Talapas (Safari will not work), as this may help to limit the potential for someone to misuse your credentials. Bear in mind that computing services can be costly so there is more at risk than your personal info (and data).

In the browser window, go to:
<https://talapas-ln1.uoregon.edu>

Enter your username and password. For UO users, your username on Talapas will be your Duck ID. That is, if your email address is alice@uoregon.edu, your Talapas username will be "alice". Your password is the same university-wide, and can be managed at the UO password reset page. If you don't know your credentials (or if you're not sure you have credentials), visit [this page](https://hpcf.uoregon.edu/content/request-access) to request access. This will require the approval of a lab PI (Condon or Weston). Since there are fees associated with using the computing cluster, your request will be evaluated based on need and the availability of other options.

There is a brief overview of the OnDemand service worth reading --- see [here](https://hpcrcf.atlassian.net/wiki/spaces/TCP/pages/922746881/Open+OnDemand).

##### Loading files for Interactive Access

Once you have logged in, it's fairly intuitive to navigate the dropdown menus at the top of the browser window. The 'Files' dropdown gives several options and each will open a new window. For shared projects, consider using the '/projects/pielab/shared' directory to store your files; otherwise use the directory associated with your username *within the pielab directory* (in other words, this one: '/projects/pielab/[username]'). Within the correct folder, you will want to create a new folder that is specific to each project as this is where you'll store the input and output files, just as you would if working on your own hard drive.

##### To launch an interactive session

From the OnDemand landing page, click 'Interactive Apps'/'Talapas Desktop'. This will load a form that requires entry of the PIRG name (pielab) and a few other fields. There are several things to keep in mind when filling out the form to launch the virtual desktop on Talapas. First, the 'partition' field requires selection of one of several options. For a complete list, with associated specs, limitations, and restrictions, see [here](https://hpcrcf.atlassian.net/wiki/spaces/TCP/pages/7285967/Partition+List). For many (most?) jobs, the default 'interactive' partition should be fine. For more intense jobs, consider using 'short' (gives up to 24 hours) or 'long' (up to 2 weeks). Note that 'interactive' has a max of 4 CPUs, which equates to about 16G RAM. For reference, a souped up laptop might have 32G and a standard MacBook Pro has 16G or maybe 8G if older. Analyses of SAPA data from 2017 or later will routinely kill RStudio with only 16G of RAM (necessitating use of the 'short' or 'long' partitions).

For the number of hours, a good practice is to use the lesser of the max amount of time (this depends on the partition) or a generous guess at the length of time needed. If the analysis runs for a long while and then times out, you will have no output and will have spent the funds anyway. Better to have a chance of getting what you need than running out of time. However, you should also get into the practice of deleting instances that are no longer in use, as this will save money! Otherwise, the expenses will add up until the full time allotment has expired. For the number of cores and total memory, the standard seems to be 4G of memory for each CPU though some partitions (fat and longfat) have CPUs with more memory --- choose the CPUs accordingly (as best you can). Note that you can also use GPUs, which seem to have more memory (and cost more). See [here](https://hpcrcf.atlassian.net/wiki/spaces/TCP/pages/364773381/Memory) for more info about guessing the right specifications. 

For SAPA processing, I have done lots of experimenting. Unfortunately, most of the analyses conducted on these data are not able to be parallelized, and this includes the most computationally expensive step of getting the count of pairwise administrations across all items. This means the marginal benefit of invoking additional CPUs is often small (but not zero). When going from raw data to a version that is Dataverse-ready, this set-up seems to work pretty well: 0 GPU, 256 GB, 9 cores, on the preempt partition for at least 24 hours. 

Note that if you seek to use more than 128 GB (as above), your request will end up being completed on the GPU partition (which has 256 GB per node) or the fat/longfat/preempt partitions (which can handle up to 200 GB, per my correspondence with the RACS team). As of July 2019, the gpu partition costs twice as much as the short partition ($0.008 per SU) and the fat partition costs 6x as much. I'm not sure how much the preempt partition charges but it's probably in the same range. The preempt partition is nice because it will typically start more quickly than if you use one of the others, though you run the risk of having the job killed if traffic on Talapas picks up among higher-priority users. See [here](https://hpcrcf.atlassian.net/wiki/spaces/TCP/pages/733184001/How-to+Use+the+preempt+Partition) for more info. This won't happen with fat or longfat, but you might have to wait a while before your job can start.

##### To determine the memory usage of jobs previously run

This has to be done through an ssh interface with Talapas. Open a shell and enter this at the prompt:


```ssh
ssh username@talapas-ln1.uoregon.edu
```
followed by your password.

To see the memory usage of recent jobs (since midnight of the current day), enter:


```summary
sacct --format='JobID,Elapsed,MaxRSS'
```

To get more information on an individual job (recommended), enter:


```info
seff <JobID>
```

That last command will return something like:


```seff
$ seff 9609990

Job ID: 9609990
Cluster: mycluster
User/Group: username/talapas
State: CANCELLED (exit code 0)
Nodes: 1
Cores per node: 8
CPU Utilized: 00:23:25
CPU Efficiency: 3.10% of 12:36:16 core-walltime
Job Wall-clock time: 01:34:32
Memory Utilized: 29.12 GB
Memory Efficiency: 91.00% of 32.00 GB
```

This job was cancelled after repeated efforts to compile. Note the high ratio of Memory Utilized to Memory Available. It is also possible to learn much more. Try using the code below by entering your own 'username' and a date that goes back a few days in place of 'year-mo-da'.


```more
sacct -u <username> -S <year-mo-da> --format='JobID,Partition,State,AllocCPUS,ReqMem,MaxRSS,TimeLimit,Elapsed'
```

This gives all of the most relevant info (in my opinion) on jobs from the date entered until now, including the final status of the job.

To check on memory usage while a job is running, you can enter 'top' in the terminal window to see info about the CPUs currently in usage. Note that you will see slightly different info if you do this through a remote login to the terminal window vs opening a terminal window within the 'live interface' (see below for more about this option).

Finally, it is also possible to obtain information about specific files. This is useful if trying to determine how much time was needed to generate an output file. From the terminal, try a command like this:


```fileinfo
ls -l ~/projects/<filename>
```

This will give the size of the file along with the date and time of creation.

##### To run a live session of RStudio

Once you have begun the session (i.e., submitted the form), a new page will load. From here, click the blue button that says 'Launch noVNC in New Tab'. This button may not be visible right away as you sit in the queue, waiting for the necessary resources to become available. When you launch the tab, a virtual desktop will open with a dropdown menu in the upper left called 'Applications'. Choose 'Education'/'Talapas RStudio'. Presumably you can figure out how to manage your workflow from here. You can also open a terminal window through this interface that will allow you to access the node you're running. To do this, click on the terminal icon in the 'TurboVNC' tab --- it's to the right of the 'Applications' dropdown menu.

##### Ending your interactive session

Your analyses will continue running until completed, timed-out, or stopped for some other reason (coding errors, etc.). When your analyses are done, you should return to the Open OnDemand main page and click the red 'Delete' button. This will stop your usage of the system and associated fees.

#### Using Talapas for Batch Jobs

I haven't done this yet (on Talapas)! But see [here](https://hpcrcf.atlassian.net/wiki/spaces/TCP/pages/7286491/How-to+Submit+a+Job) if you want to give it a go.

## Server

Files can be shared among lab members using the lab network drive. 

### Accessing the drive on a Mac

1. Go to 'Connect to Server'.
2. If you're off-campus, connect to the UO VPN.
3. Enter the network address: `smb://cas-fs2.uoregon.edu/Psychology/a/PIElab`. (It's worth adding this as a favorite network so you don't have to remember the address again.)
4. Enter your DuckID and your password when prompted. Note that you can only gain access if you have been approved for access. 

### Accessing the drive on a PC

1. Follow directions [here](https://casit.uoregon.edu/faq/mapping-file-shares-in-windows-10).

## Website

### Details

URL: [pielab-science.com](https://pielab-science.com)

Username and password: email Sara or David for this information.

### Purpose

PR for the PIE lab
 - Who's part of the PIE lab
 - What are we currently doing?
 - (If actively recruiting) landing page for new recuirts
 - (If ongoing study) landing page for study participants
 
### Current sections

- [What we study](https://pielab-science.com/research)
- About
- Current lab members (with a page for each)
- Friends of the lab
- [Cooling on the rack](https://pielab-science.com/blog/) (news)
 
### How to update
  - Go to [pielab-science.com/admin](https://pielab-science.com/admin) and log in (see above for username/password details)
  - See sections below for updating specific aspects

#### Your profile
 - Go to the Media section (on the left-hand menu) and click Add New
 - Drop file into box, or select using menus
 - Go to Pages (left-hand menu) and hover over your page -- select Edit with Elementor
 - Use the interface to change text, upload a new picture, include links to other pages, whatever you want!
 - Be sure to click Update before leaving the page.
  
#### Your CV
 - Go to the Media section (on the left-hand menu) and click Add New
 - Drop file into box, or select using menus
 - Go to Pages (left-hand menu) and hover over your page -- select Edit with Elementor
 - Hover over the box that contains the text. A pencil will show up in the corner; click on it.
 - On the left-hand side, an Edit Text Editor menu will show up. Find the link to your CV. If you click on it, the link to the PDF will appear. You can either
       - Edit the link to match the new upload (involves changing the year and month of upload and the name of the file as it was uploaded to Wordpress), or
       - Delete the current link to the CV and add a new one with the Add Media button.
 - Be sure to click Update before leaving the page.
 
#### Troubleshooting

*If the page doesn't update*

- Wait 15 minutes and reload the webpage. 
- Clear the wordpress Cache
     - On the wordpress dashboard, click on Mangaged Wordpress (top) and select Flush Cache. This will take a minute or so.
- Clear your browser Cache
     - This will be under your browser's settings. 
     - Try opening the webpage in an incognito window as well, to see if this is a problem.

## Manual

What is the manual? You're reading it right now!

### Clone lab manual to your computer

*Notes*:

  1. *this is only available to current graduate students and PIs in the lab.*
  2. *the steps listed here only need to be followed on the first use.*

**Necessary materials:**

- Git
- GitHub account with access to [PIElab organization](https://github.com/orgs/pie-lab) 
- Rstudio that is connected to GitHub through your personal account.

1. Go to [manual repository](https://github.com/pie-lab/manual). 
2. Click on the green *Clone or download* button. 
3. Copy the link that appears. 
4. Open RStudio. Create a New Project.
5. Select Version Control and then Git. Name the project ``manual'' (so it matches the Rproj file that already exists in the repository. Save this project somewhere you will remember.

### Updating the manual [using the RStudio GUI]

**Before you make ANY changes:**

1. Open the manual RStudio project. 
2. Pull the most recent version of the manual using the blue down arrow. 

**Make any changes to the manual as you think are necessary.**

3. In the Build tab in Rstudio, click on *Build Book*.
4. In the Git tab, click Commit. In the commit message section, briefly (4-5 words max) describe the changes you made. Example: wrote updating manual section. In the window on the left, the easiest thing to do is select everything and click *Stage*. Ensure all the boxes are checked. This will be slower than only selecting the parts of the book that have changed. However, the nature of an RMarkdown book is many changes affect most parts of the book (because it changes you navigate to them). If you miss a change you have made, the book may not render properly online. Click the *Commit Button*.
5. Click on the green up arrow to push the book to GitHub, which will update the book online.

### Updating the manual [using the terminal in Rstudio]

**Before you make ANY changes:**

1. Open the manual RStudio project. 
2. In the terminal window of RStudio, pull the most recent version using this code:


```git
git pull
```


**Make any changes to the manual as you think are necessary.**

3. In the Build tab in Rstudio, click on *Build Book*.
4. In the Terminal, commit your changes. The easiest way to do this is to type:


```git
git add .
```

where the period indicate to include anything. Alternatively, you can add only specific files, if you don't want to commit everything. For example:


```git
git add file.R
```
or:

```git
git add path/file.R
```
To commit your changes, type:

```git
git commit -m "message here"
```
Be sure to include a message describing the changes. Keep the message short.

Finally upload your changes with:

```git
git push
```
You're done!

### Requesting updates

You may be unable to make changes to the lab manual because you are not authorized to make changes or don't know the answer to the question. In either of those cases, you make create an issue on the GitHub page to alert the lab to the need for additional material. To do so:

1. Go to the [Issues tab](https://github.com/pie-lab/manual/issues) on the GitHub page for the lab manual.
2. Click on New Issue and complete the form. Be sure to include as much detail as you can about the issue you have. The more detailed your request, the better the information in the manual will be. 

*Note: create one issue request for each question you have. Don't put lots of requests into a single issue.*

Other lab members can take responsibility for this issue by self-assigning the issue. Once material has been added to the manual, the member responsible for resolving the issue should reply to the original poster, including a link to the relevant section. If this meets the need of the original poster, they should reply so and the issue can be marked as closed. 



## GitHub

The lab’s website [https://github.com/pie-lab](https://github.com/pie-lab) should be used to share data and code with the world. Use public repositories to share these resources. Only share data after you’ve spoken with Sara or David; SAPA data is never shared on GitHub, but public code should either indicate that the data is embargoed or should draw data directly from the DataVerse site. 

When you share code, make sure it’s flawless, because we don’t want to distribute buggy code to the world! Have other lab members check it if possible. Ask Sara or David to get access to the lab’s GitHub.

Use your personal GitHub account to create private repositories for collaboration. Note that you will probably not be able to share SAPA data (and many other large data files) through GitHub, so work with your collaborators to set up working directories that eliminate the need for changing the data-loading code. 

## Research Assistants

### Joining the PIE lab

Undergraduate students hoping to join the PIE lab as research assistants should fill out the [application form](https://forms.gle/9BFNBrPuu7pKLhPWA). This will be checked at the beginning and end of each term. Any PIE lab PI or graduate student hoping to work with undergraduate research assistants must make time to meet with RAs regularly, train them, and provide feedback and guidance. 

There are sometimes funds available to pay for work-study students. Do not hesitate to ask about these, if you are interested in doing research. Please know that it is our strong preference to hire students who otherwise would not have the opportunity to get research experience. 

## Lab logo

Here you can download the lab logo for presentations.

* [EPS file](images/PIElab.eps)
* [JPEG file](images/PIElab.jpg)
* [PDF file](images/PIElab.pdf)
* [PNG file](images/PIElab.png)
