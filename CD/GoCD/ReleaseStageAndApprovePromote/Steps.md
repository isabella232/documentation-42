## GoCD Abstractions

**![Figure 1: GoCD Abstractions](figures/GoCD-abstractions.png)**

Although it really is a simplification, it tries to convey visually 2 very important and often misunderstood/ignored characteristics of GoCD:

* its 4 built-in powerful abstractions and their relationship: *Tasks* inside *Jobs* inside *Stages* inside *Pipelines*
* the fact that some are executed in parallel (depending on agents availability) while others sequentially:
** Multiple Pipelines run in parallel
** Multiple Stages within a Pipeline run sequentially
** Multiple Jobs within a Stage run in parallel
** Multiple Tasks within a Job run sequentially