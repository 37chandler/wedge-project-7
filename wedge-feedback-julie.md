## Feedback 

Your code opens in a slightly confusing fashion, with notebook 1A in the top level with a `submission.md`. But then another 1 notebook and another submission file in the `code` folder. It looks like the top-level `submission.md` is the one I should use, so I'm going to roll with that. (I see your explanation now that I'm reading through the markdown.)

I'm slightly confused, since it appears to me you've done the project at a B level (and taken a shot at an A), but you write
> While I contracted for an 'A' in this class, given the difficulties I faced during this project, I’ll be content with a 'C'. I gave it my best effort with the time I had available, which was limited due to several unforeseen challenges in my personal life.

When you submit your final contract, just make sure to clarify this so I know what grade you're expecting. Feel free to ask me about this in person or on Teams. Your work on 1A represents a pretty substantial time investment. I'd be fine calling this a B+ Wedge project. If you did 4 of the A/B choice assignments I'd be happy to give you an A- overall. Just let me know what you're thinking. 

Nice work on this project, you can consider it complete. I'm going to read your files in order and give you feedback
as I move through them, from Task 1 to Task 3. 

One high-level point: all of your committed notebooks have runtime errors or places where you've stopped execution. Just run everything through for assignments so I
can see that it worked. Outside of classes, just clear all output and do the save and commit. 


### Task 1

* Nice job on this task. Very efficient implementation. None of the struggles you've alluded to are obvious from the finished code. 

I'd be _extremely_ careful with lines like this: 

```
    for col in numeric_columns:
        if col in df.columns:
            df[col] = df[col].fillna(0)
``` 
There are some cases where zero makes sense for an NA but many many cases where it doesn't. 


### Task 2

This notebook could use some cleaning. Drop the unneeded 25220 example and move all your imports to the top. 

You write

```
HAVING COUNT(trans_no) <= 99000 -- Keep owners with <= 99,000 transactions
```

This comment doesn't do much for me. That comment is pretty obvious to someone who reads SQL. What'd be nice is to have a comment that explains why you'd filter out those owners. I was a pretty heavy shopper and have about 12K rows. But a family who is in town year around could hit this total. 

Later you write `AND trans_status NOT IN ('R', 'V')  -- Exclude returns and voids`. This is an error. We're trying to get a sample of owner records. So, for instance, we might use this to get an estimate of the number of voids different cashiers have. This exclusion would prevent us from doing that. Plus, we couldn't recreate actual spend totals, since erroneous rings wouldn't have their voids. 

Everything else in this one is very nice. 

### Task 3

* Nice job on this, very efficient. 
* You were one of the few to get the queries right. Great job!
