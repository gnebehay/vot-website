---
template: page2023.pug
submenu: Participate
---

## Problem statement

VOTS adopts a general problem formulation that covers single/multiple-target and short/long-term tracking as special cases. The tracker is initialized in the first frame by segmentation masks for all tracked targets. In each subsequent frame, the tracker has to report all segmentation masks (one for each target). The following figure summarizes the tracking task.

![Problem statement](problem_statement.png)

## Participation steps
 
The VOTS2023 challenge took place between May 4th and June 18th 2023. After the results have been processed and analyzed by the VOTS2023 challenge committee, 47 tracker were accepted to the VOTS2023 challenge official leaderboard. To facilitate development the challenge has reopened as a VOTS2023 benchmark for the research community with the VOTS2023 challenge trackers indicated in the public leaderboard.

 - Follow the guidelines to integrate your tracker with the [new VOT toolkit](/howto/integration_multiobject.html) and [run the experiments](/howto/overview.html).
 - Register your tracker on the [registration page](https://forms.gle/YjQUsJnBN9DNod386), fill-out the tracker description questionnaire and submit the tracker description documents: a short description for the results paper and a longer description (see explanations below).
 - Once registered, submit the output produced by the toolkit ([see toolkit tutorial](https://www.votchallenge.net/howto/overview.html)) to the [evaluation server](https://eu.aihub.ml/competitions/201). Do not forget to pack the results with the `vot pack` command.
 - Receive performance scores via email. 

![Participation steps](participation_steps.png)

## VOTS Datasets

 - The VOTS *development dataset* is composed of 4 sequences with each frame accompanied by a ground truth. This dataset is meant only for development purposes, i.e., to test your tracker integration, you can also test performance evaluation, but the scores are NOT official and have no significance due to small sequence count. To run your tracker on this dataset, create the workspace using command `vot initialize tests/multiobject` and follow the remaining of the instructions in the [toolkit overview tutorial](/howto/overview.html).

 - The *VOT2023 competiton dataset* is composed of 144 sequences with ground truth only available at initialization frames. This dataset is used for tracker evaluation. Run your tracker on this dataset by creating a workspace using `vot initialize vots2023` in the toolkit and submit the output masks to the VOTS2023 evaluation server. Note that you cannot run evaluation locally on your computer for this dataset, since the ground truth is only available on the evaluation server.


### Additional clarifications
 
 - The short tracker description should contain a concise description (LaTeX format) for the VOT results paper appendix (see examples in Appendix of a VOT results papers). The longer description will be used by the VOTS TC for result interpretation. Write the descriptions in advance to speed up the submission process.
 - Results for a single registered tracker may be submitted to the evaluation server at most 10 times, each at least 24h apart to mitigate overfitting attempts. In response to submissions >10, an email  with Subject “Maximum number of VOTS submissions reached” will be sent to avoid confusion about the situation. Registering a slightly modified tracker to increase the number of server evaluations is prohibited. The VOTS committee reserves the discretion to disqualify trackers that violate this constraint. If in doubt whether a modification is “slight”, contact the VOTS committee.
 - When  coauthoring multiple submissions with similar design, the longer description should refer to the other submissions and clearly expose the differences. If in doubt whether a change is sufficient enough, contact the organisers. 
 - Authors are encouraged to submit their own previously published or unpublished trackers.
 - Authors may submit modified versions of third-party trackers. The submission description should clearly state what the changes were. Third-party trackers submitted without significant modification will not be accepted.
 - The VOTS2023 winner is required to publicly release the pretained tracker and the source code. In case private training sets are used, the authors are strongly encouraged to make the publicly available to foster results reproducibility.


### Tracker registration checklist (prepare in advance)

- Tracker long name
- Tracker short name
- Authors, affiliations + emails
- Short tracker description for the results paper appendix. See examples in the [VOT2022 results paper](https://prints.vicos.si/publications/files/416). (~800 characters with spaces when compiled, which is ~1500 characters of LaTeX text without bibtex file)
- Long tracker description (should detail the main ideas)
- Bibtex file for the long and short tracker description
- A link to the tracker code placed in a persistent depository (Github, dropbox, Gdrive,...). If the link is not yet publicly accessible, provide a password. Note that to become a co-author of the results paper, the tracker has to be publicly accessible by the VOTS2023 workshop date.

## FAQ

  - **Does the number of targets change during tracking?**

    All targets in the sequence are specified in the first frame. During tracking, some targets may disappear and possibly reappear later. The number of targets is different from sequence to sequence.

  - **Can I participate with a single-target tracker?**

    Sure, with a slight adjustment. You will write a wrapper that creates several independent tracker instances, each tracking one of the targets. To the toolkit, your tracker will be a multi-target tracker, while internally, you’re running independent trackers. See the examples [here](https://github.com/votchallenge/integration/blob/master/python/). 

  - **Can I participate with a bounding box tracker?**

    Sure, with a slight extension. In previous VOT challenges we showed that box trackers achieve very good performance on segmentation tasks by running a general segmentation on top of a bounding box. So you can simply run AlphaRef (or a similar box refinement module like SAM) on the top of your estimated bounding box to create the per-target segmentation mask. Running a vanilla bounding box tracker is possible, but its accuracy will be low (robustness might still be high). 

  - **Which datasets can I use for training?**

    Validation and test splits of popular tracking datasets are NOT allowed for training the model. These include: OTB, VOT, ALOV, UAV123, NUSPRO, TempleColor, AVisT, LaSOT-val, GOT10k-val, GOT10k-test, TrackingNet-val/test, TOTB.
    Other than above, training splits of any dataset is allowed (including LaSOT-train, TrackingNet-train, YouTubeVOS, COCO, etc.). For including the transparent objects, it is allowed to use the Trans2k dataset. In case private training sets are used, we strongly encourage making them publicly available for results reproduction. 

  - **Which performance measures are you using?**

    New performance measures are developed for the VOTS challenges, [here is a draft](https://data.votchallenge.net/vots2023/measures.pdf).

  - **When will my results be publicly available?**

    The results for a registered tracker are revealed to the participant via an email in approximately 30 minutes after submission. Considering many requests, we decided to also reveal all results in the week after the challenge closes. The leaderboard data will contain also tracker registration details (without participants personal details, long tracker description and source code password). Note that public link to the source code is mandatory for the results paper coauthorship, but can be kept under password (revealed only to VOTS committee) until the VOTS workshop.
  
  - **Why is the analysis computed with the toolkit empty?**

    The VOTS2023 public dataset contains annotations for initialization frame only, which means that the analysis cannot be computed locally by the toolkit. Thus, the results should be submitted to the server, where analysis is computed and then reported to the user via email. For mor information please see the previous post and participation instructions on this page. 

  - **If I submit several timest to the evaluation server, which submission will be used for the final score?**
    
    The **final submission** will be used for the final score. Please make sure that the tracker description matches the code that produced the final submission.

  - **Will the evaluation server remain open after the VOTS2023 deadline?**

    After the challenge deadline, the VOTS2023 challenge becomes the VOTS2023 benchmark and the evaluation server will remain open. The results submission link on the challenge page will change to enable post-challenge submissions not included in the VOTS2023 results paper. However, all benchmark and challenge submissions will appear on the same leaderboard.

<br/>
<br/>

<div class="alert alert-info" role="alert">
<div class="icon-left"><i class="glyphicon glyphicon-bullhorn hugeicon"></i> </div>
<h4>More questions?</h4>

Questions regarding the VOTS2023 challenge should be directed to the VOTS2023 committee. If you have general technical questions regarding the VOT toolkit, consult the FAQ page and the [VOT support forum](https://groups.google.com/g/votchallenge-help) first. Stay tuned with the latest VOT updates: Follow us on [Twitter](https://twitter.com/votchallenge). 
</div>



