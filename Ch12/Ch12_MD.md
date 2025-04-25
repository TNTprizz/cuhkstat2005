# Chapter 12 Markdowns
By @TNTprizz80315

# SAS: Combine Data Sets

## Concatenation
This will add the records at the bottom of a record.

```sas
DATA mged;
    SET lib1.d1(IN = IsD1) lib1.d2;
    /* If the record comes from d1, IsD1 will be 1 as a new variable. (Optional) */
RUN;
```
*Note: If the columns don't match the value, it will become a missing value.*

## Interleaving
Sorting the records based on Concatenation.

```sas
DATA emp;
    SET tsmc intel;
    BY DESCENDING salary;
    /* Just remove the DESCENDING code if you want ascending data.*/
RUN;
...
PROC SORT DATA = intel;
    BY age; /* Also does the job and apply changes to the data set. */
RUN;
```

## One-to-one Merging
Append the columns on the right of a record.

```sas
...
    MERGE D1 D2;
RUN;
```
*Note: The merging goes from the top.*  
*Note: The data will be overwritten if overlapped, which `D2` have a larger priority, even when the data in D2 is a missing value.*

## Matched Merge
One-to-one merging, but it automatically generate a new record if overlapped to include all combinations and avoid data overwritting.

```sas
...
    MERGE D1 D2;
    BY DESCENDING A;
    /* The generation will be based on A.*/
RUN;
```

## Updating
Will only apply changes from a data set, ignoring the missing values.

```sas
...
    UPDATE emp salary_change;
    BY staff_id;
RUN;
```
*Note: New data can be added by adding items in the transac data set.*

## Remarks
 - There can be more than one sorting options in the `BY` statement, but it must exist in the data sets being merged.
 - You can process the reslutant data after combining the data.