## Google fuzzbench, from start to finish

In this blog post we will have a look into the Google fuzzbench service. A benchmark service to evaluate fuzzers.

Currently many of the state-of-the-art fuzzers are integrated into this service. 
A security researcher or computer scientist may want to evaluate the fuzzer his working on to see how it performs on real-world targets.

I'm going to cover the following topics in general about fuzzbench :

-  What is Google Fuzzbench?
-  How fuzzbench is working?
-  Why I need to evaluate my fuzzer?
-  What targets fuzzbench supported?
-  How fuzzbench measure the code coverage?
-  Does fuzzbench support evaluating fuzzer by the factor of bug coverage?
-  How to integrate your fuzzer into fuzzbench?
-  How to request an experiment from Fuzzbench?
-  How to build and run a local experiment with fuzzbench in your system?

### What is Google Fuzzbench?

In 2 March 2020 Google has been announced that the official fuzzing benchmark service has been launched.
According to Google blog : 

Fuzzbench is  *a fully automated, open source, free service for evaluating fuzzers. The goal of FuzzBench is to make it painless to rigorously evaluate fuzzing research and make fuzzing research easier for the community to adopt.* [1]

As a simple definition, you can assume the Fuzzbench service as the best fully automated benchmark tool to evaluate your fuzzer in terms of code coverage.

Fuzzbench can be assumed as the first tool to measure and evaluate the fuzzers at scale. with the capability of their cloud systems, this service is able to evaluate unlimited number of fuzzers at the same time and the architecture is well designed. this is probably hard to be happend in your local server or machine due to the resource limitation.


### How fuzzbench is working?
Fuzzbench works by integrating the fuzzer in an easy way, build and run the instances of every fuzzer in a separate Docker. 
If you don't know what a Docker is then, this is the simplest definition : Docker is a set of platform as a service (PaaS) products that use OS-level virtualization to deliver software in packages called containers.[6] Containers are isolated from one another and bundle their own software, libraries and configuration files; they can communicate with each other through well-defined channels.[7] All containers are run by a single operating system kernel and therefore use fewer resources than virtual machines.[2]


