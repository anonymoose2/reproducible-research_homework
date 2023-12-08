# Reproducible research: version control and R

\# INSERT ANSWERS HERE #

**Question 4**

**a)** Execute the code to produce the paths of two random walks. What do you observe? (10 points)

Both Graphs maps the trajectory of an object/organism across 2-dimensional space, measured as its x and y cooridnates within this space, with time denoted by the gradient of blue of the trajectory line, from the start to the end of the walk.
There is minimal similarity between the two walks, with any clustering occuring my chance.
Each time the code is run, new plots are generated.
Each walk is comprised of 500 steps, with each step being the result of a runif function which gives steps of an equal distance, but in a randomised direction. This randomised direction or 'angle' relative to the last point, is a result of random numbers being generated for the x and y coordinates, within the range of 0 and 2pi. This change in direction or 'angle' is purely the magnitude of change in direction of x relative to y, with the distance being h (the hypotenuse), which is kept constant at 0.25. The time for each step is kept equal to the number of steps that have been taken at that point. 
Both plots use the same code and functions so are the result of the same process, but giving differnt outputs due to this randomisation of values.
Overall, this represnts a random process.

**b)** Investigate the term **random seeds**. What is a random seed and how does it work? (5 points)

A random seed, is an initialising value for a pseudo-random number generator. This is used to ensure  the same values follow the seed value, meaning you can simulate a random process, while keeping it repeatable and reproducible. For example, if the seed (input) value is kept the same, the output values will be random, but will be the same every time, given that the seed value is the same. In the context of this code, this can be added using the set.seed() function before the for loop, for example i arbritraily chose the number 7 for my seed value, giving set.seed(7), this resulted in the same random walk output on the graphs.
Overall, using random seeds makes the process/ the code reproducible.

**c)** Edit the script to make a reproducible simulation of Brownian motion. Commit the file and push it to your forked `reproducible-research_homework` repo. (10 points)

It edited the script to include the set.seed() line of code. This is representative of brownian motion, which is a random process.
This can be found in my repository as Question 4 code edits.R

**d)** Go to your commit history and click on the latest commit. Show the edit you made to the code in the comparison view (add this image to the **README.md** of the fork). (5 points)

![image](https://github.com/eevtaylor/reproducible-research_homework/assets/150136026/b4bc5bef-ca6d-4228-82df-87521adb3084)


**Question5**

**a)** Import the data for double-stranded DNA (dsDNA) viruses taken from the Supplementary Materials of the original paper into Posit Cloud (the csv file is in the `question-5-data` folder). How many rows and columns does the table have? (3 points)

33 rows (not including the heading row) and 13 columns 

**b)** What transformation can you use to fit a linear model to the data? Apply the transformation. (3 points)

There are multiple ways to transform data, but I will use a log transformation, which is in line with what the researchers did in the original paper. Log transforming this data helps to deal with the exponential value of a (alpha) in the equation. Copied below is the code I used for this:

data$log.Virion.volume..nm.nm.nm. <- log(data$Virion.volume..nm.nm.nm.)
data$log.Genome.length..kb. <- log(data$Genome.length..kb.)

This means that LnL can be plotted against LnV, from the equation V=BL^a

I fitted the linear model as so:

model <- lm(log.Virion.volume..nm.nm.nm. ~ log.Genome.length..kb., data = data)
summary(model)


**c)** Find the exponent ($\alpha$) and scaling factor ($\beta$) of the allometric law for dsDNA viruses and write the p-values from the model you obtained, are they statistically significant? Compare the values you found to those shown in **Table 2** of the paper, did you find the same values? (10 points)

The output of the linear model gave an intercept of exp(7.0748) = 1181.807 which is the β value. 
The slope is given as 1.5152 which is the 𝛼 value.

The p values for both 𝛼 and β, are low (2.28e-10 and 6.44e-10 respectively), which is statistically significant.

These values are the same as the ones found in Table 2 of the original paper

**d)** Write the code to reproduce the figure shown below. (10 points)

ggplot(data, aes(x = log(data$Genome.length..kb.) , y = log(data$Virion.volume..nm.nm.nm.))) +
  geom_point() +
  labs(x = "log[Genome length(kb)]", y = "log[Virion volume(nm3)]")+
  geom_smooth(method="lm", se= T) +
  theme_bw()+
  theme(
    text = element_text(face = "bold")
  )

See below for the matching figure:
![986dafef-7158-4839-84e6-2d4c8c5e07e1](https://github.com/eevtaylor/reproducible-research_homework/assets/150136026/cca195fd-8bdc-4548-bfd5-ba020cfea22c)


**c)** What is the estimated volume of a 300 kb dsDNA virus? (4 points)

equation= V = βL^α
a= 1.5152 β=7.0748 L=300
V=6697007

TMy estimate for the volume of a 300kb dsDNA visrus is 6697007 nm^3

**Bonus** (**10 points**) Explain the difference between reproducibility and replicability in scientific research. How can git and GitHub be used to enhance the reproducibility and replicability of your work? what limitations do they have? (e.g. check the platform [protocols.io](https://www.protocols.io/)).

Reproducability is the abilty to repeat the same data and the same methodology, and obtain the same results.

Replicability is whether the same conclusions can be drawn, using different data,  to answer the same research question.

Git and Github, being the software and website respectively, are important tools for imporving reproducibility and replicability in the scientific field.

Firstly, Github allows for effective version control. This measns that any changes to data/code can be tracked, avoiding the risk of writing over old code. This also allows others to understand how the code has evolved over time.

Secondly, the fact that github has oopen access means that other researchers can access code, which they can review, build upon or use as guidance, therefore increasing replicability. 

Additionally, Github allows engagement from across the sceintific community, which can faciliate better communication and aknowledgement across work. However, one limitation in this area is the github is not very user-friendly, which could put off first time users, limiting the benefits of this community engagement.

Github allows for branching and merging of documents/repositories, this means that different versions can be worked on, and tested for reproducibility and replicability. 

Github also icnreases the replicability and reprodcibility by being an online, cloud- based platform. This means that the code and data is not tied to a particular desktop, which puts it at risk of being lost. However, one limitation with this is that an internet required to access Github, meaning it may not be practical in some situations, such as during remote fieldwork.


## Instructions

The homework for this Computer skills practical is divided into 5 questions for a total of 100 points (plus an optional bonus question worth 10 extra points). First, fork this repo and make sure your fork is made **Public** for marking. Answers should be added to the # INSERT ANSWERS HERE # section above in the **README.md** file of your forked repository.

Questions 1, 2 and 3 should be answered in the **README.md** file of the `logistic_growth` repo that you forked during the practical. To answer those questions here, simply include a link to your logistic_growth repo.

**Submission**: Please submit a single **PDF** file with your candidate number (and no other identifying information), and a link to your fork of the `reproducible-research_homework` repo with the completed answers. All answers should be on the `main` branch.

## Assignment questions 

1) (**10 points**) Annotate the **README.md** file in your `logistic_growth` repo with more detailed information about the analysis. Add a section on the results and include the estimates for $N_0$, $r$ and $K$ (mention which *.csv file you used).
   
2) (**10 points**) Use your estimates of $N_0$ and $r$ to calculate the population size at $t$ = 4980 min, assuming that the population grows exponentially. How does it compare to the population size predicted under logistic growth? 

3) (**20 points**) Add an R script to your repository that makes a graph comparing the exponential and logistic growth curves (using the same parameter estimates you found). Upload this graph to your repo and include it in the **README.md** file so it can be viewed in the repo homepage.
   
4) (**30 points**) Sometimes we are interested in modelling a process that involves randomness. A good example is Brownian motion. We will explore how to simulate a random process in a way that it is reproducible:

   - A script for simulating a random_walk is provided in the `question-4-code` folder of this repo. Execute the code to produce the paths of two random walks. What do you observe? (10 points)
   - Investigate the term **random seeds**. What is a random seed and how does it work? (5 points)
   - Edit the script to make a reproducible simulation of Brownian motion. Commit the file and push it to your forked `reproducible-research_homework` repo. (10 points)
   - Go to your commit history and click on the latest commit. Show the edit you made to the code in the comparison view (add this image to the **README.md** of the fork). (5 points)

5) (**30 points**) In 2014, Cui, Schlub and Holmes published an article in the *Journal of Virology* (doi: https://doi.org/10.1128/jvi.00362-14) showing that the size of viral particles, more specifically their volume, could be predicted from their genome size (length). They found that this relationship can be modelled using an allometric equation of the form **$`V = \beta L^{\alpha}`$**, where $`V`$ is the virion volume in nm<sup>3</sup> and $`L`$ is the genome length in nucleotides.

   - Import the data for double-stranded DNA (dsDNA) viruses taken from the Supplementary Materials of the original paper into Posit Cloud (the csv file is in the `question-5-data` folder). How many rows and columns does the table have? (3 points)
   - What transformation can you use to fit a linear model to the data? Apply the transformation. (3 points)
   - Find the exponent ($\alpha$) and scaling factor ($\beta$) of the allometric law for dsDNA viruses and write the p-values from the model you obtained, are they statistically significant? Compare the values you found to those shown in **Table 2** of the paper, did you find the same values? (10 points)
   - Write the code to reproduce the figure shown below. (10 points)

  <p align="center">
     <img src="https://github.com/josegabrielnb/reproducible-research_homework/blob/main/question-5-data/allometric_scaling.png" width="600" height="500">
  </p>

  - What is the estimated volume of a 300 kb dsDNA virus? (4 points)


