# Practical Session #1: Introduction

1. Find in news sources a general public article reporting the discovery of a software bug. Describe the bug. If possible, say whether the bug is local or global and describe the failure that manifested its presence. Explain the repercussions of the bug for clients/consumers and the company or entity behind the faulty program. Speculate whether, in your opinion, testing the right scenario would have helped to discover the fault.

2. Apache Commons projects are known for the quality of their code and development practices. They use dedicated issue tracking systems to discuss and follow the evolution of bugs and new features. The following link https://issues.apache.org/jira/projects/COLLECTIONS/issues/COLLECTIONS-794?filter=doneissues points to the issues considered as solved for the Apache Commons Collections project. Among those issues find one that corresponds to a bug that has been solved. Classify the bug as local or global. Explain the bug and the solution. Did the contributors of the project add new tests to ensure that the bug is detected if it reappears in the future?

3. Netflix is famous, among other things we love, for the popularization of *Chaos Engineering*, a fault-tolerance verification technique. The company has implemented protocols to test their entire system in production by simulating faults such as a server shutdown. During these experiments they evaluate the system's capabilities of delivering content under different conditions. The technique was described in [a paper](https://arxiv.org/ftp/arxiv/papers/1702/1702.05843.pdf) published in 2016. Read the paper and briefly explain what are the concrete experiments they perform, what are the requirements for these experiments, what are the variables they observe and what are the main results they obtained. Is Netflix the only company performing these experiments? Speculate how these experiments could be carried in other organizations in terms of the kind of experiment that could be performed and the system variables to observe during the experiments.

4. [WebAssembly](https://webassembly.org/) has become the fourth official language supported by web browsers. The language was born from a joint effort of the major players in the Web. Its creators presented their design decisions and the formal specification in [a scientific paper](https://people.mpi-sws.org/~rossberg/papers/Haas,%20Rossberg,%20Schuff,%20Titzer,%20Gohman,%20Wagner,%20Zakai,%20Bastien,%20Holman%20-%20Bringing%20the%20Web%20up%20to%20Speed%20with%20WebAssembly.pdf) published in 2018. The goal of the language is to be a low level, safe and portable compilation target for the Web and other embedding environments. The authors say that it is the first industrial strength language designed with formal semantics from the start. This evidences the feasibility of constructive approaches in this area. Read the paper and explain what are the main advantages of having a formal specification for WebAssembly. In your opinion, does this mean that WebAssembly implementations should not be tested? 

5.  Shortly after the appearance of WebAssembly another paper proposed a mechanized specification of the language using Isabelle. The paper can be consulted here: https://www.cl.cam.ac.uk/~caw77/papers/mechanising-and-verifying-the-webassembly-specification.pdf. This mechanized specification complements the first formalization attempt from the paper. According to the author of this second paper, what are the main advantages of the mechanized specification? Did it help improving the original formal specification of the language? What other artifacts were derived from this mechanized specification? How did the author verify the specification? Does this new specification removes the need for testing?

## Answers

1. On 20minutes, a French news website, we found an article about a bug in the Firefox browser. 

source : https://www.20minutes.fr/high-tech/4017153-20230103-bug-enfin-corrige-firefox-18-ans-apres-decouverte
https://bugzilla.mozilla.org/show_bug.cgi?id=290125

The bug was discovered in Firefox version 1.0, eighteen years ago. It affected text rendering, specifically with a style descripti²on where a large initial capital letter did not display correctly. The issue was related to the interpretation of a CSS, specifically the pseudo-element "CSS ::first-letter" when coupled with a float property. This bug is a global bug of concurrency between these two properties. According to Mozilla's tracking system, the bug was quickly discovered but  considered a non-priority, resulting in the large initial letters being displayed incorrectly on websites using Firefox and causing aesthetic problems. Despite being reported, the resolution was delayed for eighteen years. The impact was mainly visual, affecting the presentation of initial letters on certain websites (but without hindering the use of websites). The only repercussion for Mozilla could be an eventual loss of users. The bug's correction is expected with the release of Firefox 110 in next February. Testing wouldn't have been relevant in this case, because the bug was already known and just ignored.

2. "CollectionUtils.retainAll() not throwing proper NullPointerException(NPE)" is an example of issue considered as solved for the Apache Commons Collections project. The resolution of this issue is a fix.
The bug was a local bug, local to the function CollectionUtils.retainAll(). The bug was that the function did not throw a NullPointerException when one of its parameters was null, contrary to what was specified in the documentation. 
The bug was patched by throwing a NullPointerException when one of the parameters is null (and updating the comments). In the commit, we can see that the same patch has also been made in several other functions of the same class.
The contributor added new tests to verify that each updated function throws a NullPointerException when one of its parameters is null (one test for each parameter), and ensure that the bug is detected if it reappears in the future.
For the function in the title of the issue, the new tests are entitled "testRetainAllNullSubColl" and "testRetainAllNullSubColl".
source : https://issues.apache.org/jira/projects/COLLECTIONS/issues/COLLECTIONS-813?filter=doneissues


-------------
. Read the paper and briefly explain what are the concrete experiments they perform, what are the requirements for these experiments, what are the variables they observe and what are the main results they obtained. Is Netflix the only company performing these experiments? Speculate how these experiments could be carried in other organizations in terms of the kind of experiment that could be performed and the system variables to observe during the experiments.
-------------

3. The concrete experiments performed by Netflix are the following:

- Chaos Monkey: Randomly terminates virtual machine instances that host production services during normal working hours. 

- Chaos Kong: Simulates the failure of an entire Amazon EC2 region..

- Failure Injection Testing (FIT) exercises: Cause requests between Netflix services to fail deliberately and verify that the system degrades gracefully.

REQUIREMENTS: ?????????????

VARIABLES : ???

main results : ????

how these experiments could be carried in other organizations : ???


/!\ Source chatGPT /!\

However, I can provide you with a general overview of Chaos Engineering based on what was known up to my last update. Netflix, along with other tech companies, popularized Chaos Engineering as a fault-tolerance verification technique. The general idea is to intentionally introduce failures and disruptions in a controlled environment to observe how the system responds, with the goal of improving overall resilience.

Typically, in Chaos Engineering, companies might perform experiments like:

    Simulating Server Shutdowns: Intentionally shutting down servers to observe how the system reroutes traffic and maintains service continuity.

    Network Latency Injection: Introducing artificial delays in network communication to test how the system handles slower response times.

    Database Outages: Simulating issues with databases, such as connection failures or increased response times.

The requirements for these experiments often include:

    Controlled Environment: Ensuring that the experiments are conducted in a controlled environment to minimize the impact on end-users.

    Monitoring Tools: Implementing robust monitoring tools to track system behavior and performance during experiments.

    Rollback Plans: Having well-defined rollback plans in case the introduced faults have severe consequences.

The variables observed during these experiments could include:

    System Response Time: How quickly the system can recover and resume normal operations.

    Error Rates: Monitoring the occurrence of errors and how well the system handles them.

    Resource Utilization: Observing how the system adapts to changes in resource availability.

As for whether Netflix is the only company performing these experiments, it's unlikely. Many technology companies and organizations adopt Chaos Engineering principles to enhance the reliability and resilience of their systems.

In terms of how these experiments could be carried out in other organizations, it depends on the specific context and goals. Different industries and systems may have unique requirements. Generally, organizations can start with small, controlled experiments, gradually increasing complexity as they gain confidence in their systems' resilience. Identifying critical system components and potential failure scenarios is crucial.

Keep in mind that the specific details of Netflix's experiments and results would require access to the mentioned paper or the latest information beyond my last update in January 2022.

4.
/!\ Source chatGPT /!\

I don't have direct access to specific papers, and as of my last knowledge update in January 2022, I don't have knowledge of the specific paper you're referring to about WebAssembly. However, I can provide general insights into the advantages of having a formal specification for WebAssembly.

Having a formal specification for WebAssembly offers several key advantages:

    Clarity and Precision: A formal specification provides a clear and precise definition of the language's syntax, semantics, and behavior. This clarity helps developers, implementers, and researchers understand the language specifications in a consistent and unambiguous way.

    Interoperability: Formal specifications help ensure consistency and interoperability across different implementations of WebAssembly. This is crucial for the web ecosystem, as it allows developers to write code that works consistently across various browsers and platforms.

    Verification and Validation: Formal specifications enable rigorous verification and validation processes. Implementers can use the specification as a reference to verify that their implementations adhere to the standard. This helps catch potential bugs, inconsistencies, or deviations early in the development process.

    Language Evolution: As WebAssembly evolves, a formal specification serves as a solid foundation for discussing and implementing new features. It provides a reference point for proposing changes, understanding their implications, and ensuring backward compatibility.

    Security: The formal specification helps in identifying and addressing security concerns. With a well-defined specification, security researchers can analyze the language's features and behavior systematically, leading to more secure implementations.

Now, regarding whether having a formal specification means that WebAssembly implementations should not be tested, the answer is no. While a formal specification provides a strong foundation and reduces ambiguity, it does not eliminate the need for testing. Testing remains a crucial part of the software development process to catch implementation-specific issues, performance optimizations, and other potential problems that might not be fully captured by the formal specification alone.

In summary, a formal specification for WebAssembly offers numerous benefits, including clarity, interoperability, verification, and security. However, testing remains essential for ensuring robust and reliable implementations that meet the diverse needs of the web ecosystem.