## Google fuzzbench, from start to finish

In this blog post we will have a look into the Google fuzzbench service. A benchmark service to evaluate fuzzers.

Currently many of the state-of-the-art fuzzers are integrated into this service. 
A security researcher or computer scientist may want to evaluate the fuzzer that he is working on to see how it performs on real-world targets.

I'm going to cover the following topics in general about fuzzbench :

-  What is Google Fuzzbench?
-  How fuzzbench is working?
-  Why I need to evaluate my fuzzer?
-  What targets fuzzbench supported?
-  The benefits of using Google fuzzbench
-  How fuzzbench measure the code coverage?
-  Does fuzzbench support evaluating fuzzer by the factor of bug coverage?
-  How to integrate your fuzzer into fuzzbench?
-  How to request an experiment from Fuzzbench?
-  How to build and run a local experiment with fuzzbench in your system?
-  Troubleshooting Fuzzbench 

### What is Google Fuzzbench?

In 2 March 2020 Google has been announced that the official fuzzing benchmark service has been launched.
According to Google blog : 

Fuzzbench is  *a fully automated, open source, free service for evaluating fuzzers. The goal of FuzzBench is to make it painless to rigorously evaluate fuzzing research and make fuzzing research easier for the community to adopt.* [1]

As a simple definition, you can assume the Fuzzbench service as the best fully automated benchmark tool to evaluate your fuzzer in terms of code coverage.

Fuzzbench can be assumed as the first tool to measure and evaluate the fuzzers at scale. with the capability of their cloud systems, this service is able to evaluate unlimited number of fuzzers at the same time and the architecture is well designed. this is probably hard to be happend in your local server or machine due to the resource limitation.


### How fuzzbench is working?
Fuzzbench works by integrating the fuzzer in an easy way, build and run the instances of every fuzzer in a separate Docker. 
If you don't know what a Docker is then, this is the simplest definition : Docker is a set of platform as a service (PaaS) products that use OS-level virtualization to deliver software in packages called containers. Containers are isolated from one another and bundle their own software, libraries and configuration files; they can communicate with each other through well-defined channels. All containers are run by a single operating system kernel and therefore use fewer resources than virtual machines.[2]

This usage of Docker system, lets every fuzzer to use the available resources in a dedicated manner. avoiding conflicts with other fuzzer, hence have much realistic results .

As a simple approach, fuzzbench works as follow :
- Typically, a researcher submits a new fuzzer to the fuzzbench service and request an experiment
- Fuzzbench uses the `builder.Dockerfile` to fetch the dependencies and build the fuzzer in the right way as the fuzzer author defined .
- The fuzzbench uses the `fuzzer.py` script to prepare the environment to build the benchmarks . each specified benchmark builds as specified in the `fuzzer.py` script.
- The experiment runs for a 24 hours cycle and report about every fuzzer and requested benchmarks will be generated automatically.

### Why I need to evaluate my fuzzer?
Hopefully, fuzzbench is not limited to evaluate your fuzzer. you can experiment different fuzzers in this platform but generally the use cases are :
- Evaluate the effectiveness of your research prototype of different real-world targets.
- Compare the throughput of different fuzzer in a similar condition .
- Evaluate a specific feature in a fuzzer in scale before submiting the patch and push it into the master branch.
- Improve your fuzzer by evaluating different fuzzers functionality and stability in different benchmarks .
- Select the best available fuzzer to run a fuzzing campaign to detect potential vulnerability in a specific target

So, generally fuzzbench lets you do a precise and fair evaluation between different fuzzers and real-world targets.


### What targets fuzzbench supported?
Currently the following benchmarks or targets are available :
- bloaty_fuzz_target
- curl_curl_fuzzer_http
- freetype2-2017
- harfbuzz-1.3.2
- harfbuzz_hb-subset-fuzzer
- jsoncpp_jsoncpp_fuzzer
- lcms-2017-03-21
- libhevc_hevc_dec_fuzzer
- libjpeg-turbo-07-2017
- libpcap_fuzz_both
- libpng-1.2.56
- libxml2-v2.9.2
- libxslt_xpath
- matio_matio_fuzzer
- mbedtls_fuzz_dtlsclient
- ndpi_fuzz_ndpi_reader
- openh264_decoder_fuzzer
- openssl_x509
- openthread-2019-12-23
- php_php-fuzz-parser
- proj4-2017-08-14
- re2-2014-12-09
- sqlite3_ossfuzz
- stb_stbi_read_fuzzer
- systemd_fuzz-link-parser
- vorbis-2017-12-11
- wabt_wasm2wat_fuzzer
- woff2-2016-05-06
- zlib_zlib_uncompress_fuzzer

### The benefits of using Google fuzzbench
It's a free service, even if you request the Google fuzzbench team to run a private experiment for you. using the Google resources to run fair evaluation on your fuzzer makes this very interesting.
At the technical side, fuzzbench is the work of some of the well-known security researchers from Google, namely Jonathan Metzman, Abhishek Arya and László Szekeres. Looking at the commits you can check that improvements, fixes and new features are done on fuzzbench as a daily basis. so you can be sure that you're using a well-cared platform.

The other benefits of using the Google fuzzbench platform is that the workflow is completely automatic. when you developed your fuzzer in the right way and integrated that into the fuzzbench the remaining steps will be done in an automatic fashion after requesting to run an experiment.

Furthermore, instead of doing a lot of hard works to setup different fuzzers on diffent machines to get the plots and making all those simple graphs, fuzzbench supports running private experiments as request. if you want to evaluate your fuzzer in a way that others would not be able to see your fuzzer codes and reports, then this option is good for you. 
For private reports, prepare your fuzzer in the fuzzbench way of integration, drop a mail to fuzzbench at google.com and if accepted then send your patch to fuzzbench team and they will run evaluations for you as requested.


### How fuzzbench measures the code coverage?
Code coverage is a vast topic, however in case of Google fuzzbench, fuzzbench uses `LLVM Code Coverage Mapping Format`. it actually is using the `-fprofile-instr-generate` clang feature to track the code coverage.
The official documentation is located [here](https://llvm.org/docs/CoverageMappingFormat.html#id14) .
The `LLVM Code Coverage Mapping Format` is working on a per-function level .

--------------
Will continue this ... waiting for fuzzbench local runs ...




### Troubleshooting Fuzzbench 
During local experiments you may face some issues. 

Here I faced some problems and I've managed to solve them. so here you can find more information about this problems and how to fix them .

- ModuleNotFoundError: No module named 'pybind11'.

This is a problem you may face during the fuzzbench installation process. 
If you started doing fuzzbench installation in the way from [fuzzbench official installation](https://google.github.io/fuzzbench/getting-started/prerequisites/), you may face this issue after running the `make install-dependencies` command. Indeed, this command will install python dependencies for required fuzzbench but if you received the mentioned error then I'm encouraging you do to the following :

	1. Please make sure that you have already python 3.8 installed, it's the minimum python version that fuzzbench needs.
	2. Run the following commands in the following order :
	`source .venv/bin/activate`
	`pip install -r requirements.txt`

	3. If you still receive error regarding installing python dependencies, then run :
	`pip install --upgrade setuptools` and after this, repeat previous step (`pip install -r requirements.txt`) .




