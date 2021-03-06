metadata for character research
===============================

There are several kinds of metadata here. Broadly, volume-level metadata, used in calculating publication statistics, and character-level metadata, used in predictive modeling.

volume-level metadata
---------------------

The metadata we're actively using is **filtered_fiction_metadata.csv**, which lists 93,708 volumes, stretching from 1800 to 2007. It focuses on fiction, but will include works in translation. It's also not restricted to "the novel"; short stories and even folktales are included. But we have tried to exclude fiction aimed explicitly at a juvenile audience across the whole timeline.

**merged_fiction_metadata** is an older version, containing more error.

There is no authoritative master list of "all English-language fiction from 1800 to the present." So scholars who want to do research at scale have to construct their own list.

Doing that by hand might take several decades. University libraries have not reliably tagged all volumes of fiction as "fiction"; you would have to actually check, book by book.

We have adopted a probabilistic solution. Using the texts of volumes, as well as existing metadata, we made reasonably good guesses about genre, and assembled a list of works *likely to be* fiction.

That means the list will contain errors: a certain number of volumes that are actually nonfiction, poetry, drama.

Here's an assessment of the error rate, based on manual sampling (a random sample of titles were eyeballed, and things clearly not fiction were tagged — raw data in **checkingforerrors.csv**). You'll notice that the timeline divides into three parts. That's not an accident! This dataset was created in three stages over a period of years (up to 1899, 1900-22, 1923-), and Underwood used slightly different filtering strategies in each stage. The upshot is that the dataset may contain 5% more biographies and travelogues, etc., in the period 1900-1922 than either before or after. If you see a pattern that could be explained by this variation, be wary.

![Error rate by 20-year periods](https://github.com/tedunderwood/character/blob/master/metadata/metadata_error.png)

Volumes are dated by date of publication, which is not guaranteed to be the date of *first* publication. We have made an effort to remove duplicates, and books published long after the death of the author. But you will still find works like *The Thousand and One Nights* that were not composed in the period 1800-2007.

There is a separate line for each volume, and the column **volid** always contains a HathiTrust Volume Identifier. The column **docid** contains a code that can be used to identify the *work,* i.e., the story in question -- which may include more than one volume, especially before 1900. If the story includes only one volume this will be identical to the **volid**.

**authgender** is author gender, which will be either m, f, or u (unknown or other). These codes should be understood as probabilistic inferences about a conventional public role, not as claims about the truth of identity. They are based for the most part on names and honorifics, but about 10% of the volumes in the dataset were also corrected by reference to metadata manually produced at Chicago, Stanford, or Illinois.

The number of volumes tagged "u" does steadily increase across time, because academic libraries bought a growing number of works translated from other languages, and our gender-inference software often confesses uncertainty about those names.

In producing **filtered_fiction** we removed 18c books. For running models, we added back 1780-1799; this metadata is in **filtered_fiction_plus_18c.tsv**.

character-level metadata
------------------------

**balanced_character_subset.csv** lists 83,920 characters used in the main modeling process that produced figure 7.

**balanced_authgender_subset.csv** list 42,928 characters used in the modeling processes that produced figures 9 and 10.
