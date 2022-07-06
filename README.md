# WinoNB Dataset

By: [Connor Baumler](https://ctbaumler.github.io/) `<baumler@umd.edu` and [Rachel Rudinger](https://rudinger.github.io/) `<rudinger@umd.edu>`

To help understand coreference systems' understanding of singular vs plural they/them pronouns, we adapted existing winograd schemas to create this dataset of **WinoNB** schemas. What follows below is the [datasheet](https://arxiv.org/abs/1803.09010) describing this data. If you use this dataset, please acknowledge it by citing the original paper:

<!-- ```
bibtex should go here
``` -->


## Motivation


1. **For what purpose was the dataset created?** *(Was there a specific task in mind? Was there a specific gap that needed to be filled? Please provide a description.)*

    This dataset was created to study how well coreference resolution systems can differentiate singular vs plural they/them pronouns in English. 
    
    Existing work considers whether models’ resolutions of they/them pronouns relies on gendered occupation stereotypes ([Rudinger et al., 2018](https://arxiv.org/abs/1804.09301)) and investigates models’ understanding of they/them pronouns in naturally occurring text ([Cao and Daumé III, 2020](https://arxiv.org/abs/1910.13913)). This dataset directly measures models’ ability to differentiate singular and plural “they”.

1. **Who created this dataset (e.g., which team, research group) and on behalf of which entity (e.g., company, institution, organization)?**
    
    This dataset was created by Connor Baumler, a graduate student at the Universtiy of Maryland (UMD).


1. **Who funded the creation of the dataset?** *(If there is an associated grant, please provide the name of the grantor and the grant name and number.)*
    
    None


1. **Any other comments?**
    
    None.





## Composition


1. **What do the instances that comprise the dataset represent (e.g., documents, photos, people, countries)?** *(Are there multiple types of instances (e.g., movies, users, and ratings; people and interactions between them; nodes and edges)? Please provide a description.)*
    
    Each instance contains a sentence with a singular entity (either named or a generic "someone") and a plural entity as well as a they/them pronoun which refers to either the singular or plural entity.


2. **How many instances are there in total (of each type, if appropriate)?**
    
    The dataset consist of 4077 templates. Each template is filled with 15 names (provided in winonb.tsv) and filled with the generic "someone" (provided in winonb_someone.tsv). 

    120 come from Winogender. 

    3722 come from WinoBias. This is more than the number of original sentences in WinoBias. Some schemas were removed entirely as we will address in the next question. For the schema that were left in, each pair of sentences could be turned in to 4 WinoNB examples as either occupation could be replaced with the singular person. For example:
   
    * [The carpenter] met with the teacher so that [she] could fix the cabinets in the classroom.
    * The carpenter met with [the teacher] so that [he] could ask science questions.
    
    could become:
    * [The carpenters] met with Riley so that [they] could fix the cabinets in the classroom.
    * The carpenters met with [Riley] so that [they] could ask science questions.
    * [Riley] met with the teachers so that [they] could fix the cabinets in the classroom.
    * Riley met with [the teachers] so that [they] could ask science questions.

    87 come from WSC. Note that this is unbalanced between the correct resolutions. WSC is not totally balances as it, on occasion, gives more than one related scenario where the resolution could go in one direction or the other. 

    148 come from DPR.


3. **Does the dataset contain all possible instances or is it a sample (not necessarily random) of instances from a larger set?** *(If the dataset is a sample, then what is the larger set? Is the sample representative of the larger set (e.g., geographic coverage)? If so, please describe how this representativeness was validated/verified. If it is not representative of the larger set, please describe why not (e.g., to cover a more diverse range of instances, because instances were withheld or unavailable).)*
    
    We pulled from our 4 source, removing schemas about non-human entities as well some schemas about scenarios that wouldn't work well with a singular and a plural entity were removed. This means that for WSC, our set of examples is not representative, but their examples about non-human entities do not help in our goal of understanding coreference resolution systems' understanding of singular they as it relates to humans. 


4. **What data does each instance consist of?** *(``Raw'' data (e.g., unprocessed text or images)or features? In either case, please provide a description.)*
    
    Each instance contains the source (Winogender, WinoBias, WSC, or DPR) of the original schema. A "sentid" gives the plural and singular participant occupation/name, the correct label, and the name-gender association. For the WinoBias examples, the sentid also lists whether it's a type 1 or type 2 example ([See the original paper for more detail](https://arxiv.org/abs/1804.06876)) and whether it was in the WinoBias dev or test set. Finally, the "sent" column gives the actual sentence containing the two entities and a they/them pronoun.


5. **Is there a label or target associated with each instance? If so, please provide a description.**
    
    In the "sentid" column, the first number (0 or 1) is the label. 1 is for the singular entity and 0 is for the plural.


6. **Is any information missing from individual instances?** *(If so, please provide a description, explaining why this information is missing (e.g., because it was unavailable). This does not include intentionally removed information, but might include, e.g., redacted text.)*
    
    None


7. **Are relationships between individual instances made explicit (e.g., users' movie ratings, social network links)?** *( If so, please describe how these relationships are made explicit.)*
    
    The "sentid"s can be used to find which sentences are fills of the same template (with different values for the name and name-gender association).


8. **Are there recommended data splits (e.g., training, development/validation, testing)?** *(If so, please provide a description of these splits, explaining the rationale behind them.)*
    
    We expect this data to be used solely for testing purposes.


9. **Are there any errors, sources of noise, or redundancies in the dataset?** *(If so, please provide a description.)*
    
    We expect that there could be some errors in number agreement as the verbs were changed to plural automatically and then corrected by hand where we found mistakes. We also expect there could be mistakes in genitive vs accusative pronouns in the examples that don't come from Winogender. The other sources do not mark the pronoun type, making it non-trivial to change from "her" into "them" or "their". We have tried to correct such mistakes by hand. 


10. **Is the dataset self-contained, or does it link to or otherwise rely on external resources (e.g., websites, tweets, other datasets)?** *(If it links to or relies on external resources, a) are there guarantees that they will exist, and remain constant, over time; b) are there official archival versions of the complete dataset (i.e., including the external resources as they existed at the time the dataset was created); c) are there any restrictions (e.g., licenses, fees) associated with any of the external resources that might apply to a future user? Please provide descriptions of all external resources and any restrictions associated with them, as well as links or other access points, as appropriate.)*
    
    The dataset is self-contained.


11. **Does the dataset contain data that might be considered confidential (e.g., data that is protected by legal privilege or by doctor-patient confidentiality, data that includes the content of individuals' non-public communications)?** *(If so, please provide a description.)*
    
    No, all scenarios are ficticious.


12. **Does the dataset contain data that, if viewed directly, might be offensive, insulting, threatening, or might otherwise cause anxiety?** *(If so, please describe why.)*
    
    Not significantly. There are some scenarios that mention death. 


13. **Does the dataset relate to people?** *(If not, you may skip the remaining questions in this section.)*
    
    No, all scenarios are ficticious.


14. **Does the dataset identify any subpopulations (e.g., by age, gender)?** *(If so, please describe how these subpopulations are identified and provide a description of their respective distributions within the dataset.)*
    
    n/a


15. **Is it possible to identify individuals (i.e., one or more natural persons), either directly or indirectly (i.e., in combination with other data) from the dataset?** *(If so, please describe how.)*
    
    n/a


16. **Does the dataset contain data that might be considered sensitive in any way (e.g., data that reveals racial or ethnic origins, sexual orientations, religious beliefs, political opinions or union memberships, or locations; financial or health data; biometric or genetic data; forms of government identification, such as social security numbers; criminal history)?** *(If so, please provide a description.)*
    
    n/a


17. **Any other comments?**
    
    None.





## Collection Process


1. **How was the data associated with each instance acquired?** *(Was the data directly observable (e.g., raw text, movie ratings), reported by subjects (e.g., survey responses), or indirectly inferred/derived from other data (e.g., part-of-speech tags, model-based guesses for age or language)? If data was reported by subjects or indirectly inferred/derived from other data, was the data validated/verified? If so, please describe how.)*
    
    The original schemas were dran from [Winogender](https://github.com/rudinger/winogender-schemas), [WinoBias](https://github.com/uclanlp/corefBias/tree/master/WinoBias/wino), [WSC](https://cs.nyu.edu/~davise/papers/WinogradSchemas/WS.html), and [DRP](http://www.hlt.utdallas.edu/~vince/data/emnlp12/).


1. **What mechanisms or procedures were used to collect the data (e.g., hardware apparatus or sensor, manual human curation, software program, software API)?** *(How were these mechanisms or procedures validated?)*
    
    Annotations were created through a mix of human editing and an adaptation of [Winogender's template script](https://github.com/rudinger/winogender-schemas/blob/master/scripts/instantiate.py)


1. **If the dataset is a sample from a larger set, what was the sampling strategy (e.g., deterministic, probabilistic with specific sampling probabilities)?**
    
    As we discussed in question #3 of [Composition](#composition), schemas about non-human entities as well some schemas about scenarios that wouldn't work well with a singular and a plural entity were removed. 


1. **Who was involved in the data collection process (e.g., students, crowdworkers, contractors) and how were they compensated (e.g., how much were crowdworkers paid)?**
    
    All annotation was done by Connor Baumler. 100 examples were hand verified by a graduate student who was compensated with a $20 gift card.


1. **Over what timeframe was the data collected?** *(Does this timeframe match the creation timeframe of the data associated with the instances (e.g., recent crawl of old news articles)?  If not, please describe the timeframe in which the data associated with the instances was created.)*
    
    The datasets we pull from were released in 2018 and 2012. The WinoNB schemas were created in 2021.


1. **Were any ethical review processes conducted (e.g., by an institutional review board)?** *(If so, please provide a description of these review processes, including the outcomes, as well as a link or other access point to any supporting documentation.)*
    
    No


1. **Does the dataset relate to people?** *(If not, you may skip the remaining questions in this section.)*
    
    No


1. **Did you collect the data from the individuals in question directly, or obtain it via third parties or other sources (e.g., websites)?**
    
    n/a


1. **Were the individuals in question notified about the data collection?** *(If so, please describe (or show with screenshots or other information) how notice was provided, and provide a link or other access point to, or otherwise reproduce, the exact language of the notification itself.)*
    
    n/a


1. **Did the individuals in question consent to the collection and use of their data?** *(If so, please describe (or show with screenshots or other information) how consent was requested and provided, and provide a link or other access point to, or otherwise reproduce, the exact language to which the individuals consented.)*
    
    n/a


1. **If consent was obtained, were the consenting individuals provided with a mechanism to revoke their consent in the future or for certain uses?** *(If so, please provide a description, as well as a link or other access point to the mechanism (if appropriate).)*
    
    n/a


1. **Has an analysis of the potential impact of the dataset and its use on data subjects (e.g., a data protection impact analysis) been conducted?** *(If so, please provide a description of this analysis, including the outcomes, as well as a link or other access point to any supporting documentation.)*
    
    n/a 


1. **Any other comments?**
    
    None





## Preprocessing/cleaning/labeling


1. **Was any preprocessing/cleaning/labeling of the data done (e.g., discretization or bucketing, tokenization, part-of-speech tagging, SIFT feature extraction, removal of instances, processing of missing values)?** *(If so, please provide a description. If not, you may skip the remainder of the questions in this section.)*
    
    Yes, schemas about non-human entities as well some schemas about scenarios that wouldn't work well with a singular and a plural entity were removed. This was done by hand.


1. **Was the "raw" data saved in addition to the preprocessed/cleaned/labeled data (e.g., to support unanticipated future uses)?** *(If so, please provide a link or other access point to the "raw" data.)*
    
    While not provided in this repo, the original schemas we pull from are all avalible from their original sources (see question #1 in [Collection Process](#collection-process))


1. **Is the software used to preprocess/clean/label the instances available?** *(If so, please provide a link or other access point.)*
    
    No


1. **Any other comments?**
    
    None.





## Uses


1. **Has the dataset been used for any tasks already?** *(If so, please provide a description.)*
    
    The dataset has been used to evaluate existing coreference systems. See the paper linked at the top for more details.


1. **Is there a repository that links to any or all papers or systems that use the dataset?** *(If so, please provide a link or other access point.)*
    
    No.


1. **What (other) tasks could the dataset be used for?**
    
    None


1. **Is there anything about the composition of the dataset or the way it was collected and preprocessed/cleaned/labeled that might impact future uses?** *(For example, is there anything that a future user might need to know to avoid uses that could result in unfair treatment of individuals or groups (e.g., stereotyping, quality of service issues) or other undesirable harms (e.g., financial harms, legal risks)  If so, please provide a description. Is there anything a future user could do to mitigate these undesirable harms?)*
    We don't expect any issues like these to arise from this dataset itself, but we would like to hilight that it is not a comprehensive dataset for testing the quality of servide coreference resoultion systems can provide for nonbinary people. It does not consider neo-pronouns or that people can switch between sets of pronouns. It also does not consider the full breadth of common nonbinary names.


1. **Are there tasks for which the dataset should not be used?** *(If so, please provide a description.)*
    
    Not to our knowledge


2. **Any other comments?**
    
    None.




## Distribution


1. **Will the dataset be distributed to third parties outside of the entity (e.g., company, institution, organization) on behalf of which the dataset was created?** *(If so, please provide a description.)*
    
    Yes, the dataset is freely available.


1. **How will the dataset will be distributed (e.g., tarball  on website, API, GitHub)?** *(Does the dataset have a digital object identifier (DOI)?)*
    
    The dataset is free to download at github.com/ctbaumler/winonb.


1. **When will the dataset be distributed?**
    
    The dataset is distributed as of June 2022 in its first version.


1. **Will the dataset be distributed under a copyright or other intellectual property (IP) license, and/or under applicable terms of use (ToU)?** *(If so, please describe this license and/or ToU, and provide a link or other access point to, or otherwise reproduce, any relevant licensing terms or ToU, as well as any fees associated with these restrictions.)*
    
    [TODO]


1. **Have any third parties imposed IP-based or other restrictions on the data associated with the instances?** *(If so, please describe these restrictions, and provide a link or other access point to, or otherwise reproduce, any relevant licensing terms, as well as any fees associated with these restrictions.)*
    
    Not to our knowledge.


1. **Do any export controls or other regulatory restrictions apply to the dataset or to individual instances?** *(If so, please describe these restrictions, and provide a link or other access point to, or otherwise reproduce, any supporting documentation.)*
    
    Not to our knowledge.


1. **Any other comments?**
    
    None.





## Maintenance


1. **Who is supporting/hosting/maintaining the dataset?**
    
    Connor Baumler is maintaining and hosting on github.


1. **How can the owner/curator/manager of the dataset be contacted (e.g., email address)?**
    
    E-mail addresses are at the top of this document.


1. **Is there an erratum?** *(If so, please provide a link or other access point.)*
    
    Currently, no. As we encounter errors, we may release (and version) future versions of the dataset. Any future versions will be avaliable in the same github repository. 


1. **Will the dataset be updated (e.g., to correct labeling errors, add new instances, delete instances')?** *(If so, please describe how often, by whom, and how updates will be communicated to users (e.g., mailing list, GitHub)?)*
    
    See previous.


1. **If the dataset relates to people, are there applicable limits on the retention of the data associated with the instances (e.g., were individuals in question told that their data would be retained for a fixed period of time and then deleted)?** *(If so, please describe these limits and explain how they will be enforced.)*
    
    n/a


1. **Will older versions of the dataset continue to be supported/hosted/maintained?** *(If so, please describe how. If not, please describe how its obsolescence will be communicated to users.)*
    
    Yes, all data will be versioned.


1. **If others want to extend/augment/build on/contribute to the dataset, is there a mechanism for them to do so?** *(If so, please provide a description. Will these contributions be validated/verified? If so, please describe how. If not, why not? Is there a process for communicating/distributing these contributions to other users? If so, please provide a description.)*
    
    Any errors may be submitted via the bugtracker on github. Larger extensions/augmentations to WinoNB may be accepted at the authors' discretion. It can be built on in the creation of other datasets freely.


1. **Any other comments?**
    
    The formatting for this datasheet was adapted from a datasheet by Trista Cao and Hal Daumé III (available [here](https://github.com/TristaCao/into_inclusivecoref/blob/master/GICoref/datasheet-gicoref.md))

