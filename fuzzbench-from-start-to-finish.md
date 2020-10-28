## Google fuzzbench, from start to finish

In this blog post we will have a look into Google fuzzbench service. A benchmark service to evaluate fuzzer.

Currently many of the state-of-the-art fuzzers are integrated into this service. 
A security researcher or computer scientist may want to evaluate the fuzzer his working on to see how it performs on real-world targets.

### What is Google Fuzzbench?

In 2 March 2020 Google has been announced that the official fuzzing benchmark service has been launched.
According to Google blog : Fuzzbench is : *a fully automated, open source, free service for evaluating fuzzers. The goal of FuzzBench is to make it painless to rigorously evaluate fuzzing research and make fuzzing research easier for the community to adopt.*