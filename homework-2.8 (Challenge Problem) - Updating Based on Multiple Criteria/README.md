

**Question**

*This problem is provided as a supplementary learning opportunity. It is more challenging that the ordinary homework. It is ungraded. We do not ask you submit an answer.*

Write an update command that will remove the "tomato.consensus" field for all documents matching the following criteria:

 - The number of imdb votes is less than 10,000
 - The year for the movie is between 2010 and 2013 inclusive
 - The tomato.consensus field is null

How many documents required an update to eliminate a "tomato.consensus" field?

NOTE: There is a dump of the video database included in the handouts for the "Creating Documents" lesson. Use that data set to answer this question.

**Answer**

```
> db.movieDetails.find(
    {'imdb.votes':{$lt:10000}, year:{$gte:2010,$lte:2013}, $and:[{'tomato.consensus':null}, {'tomato.consensus':{$exists:true}}]}
).count();
```

```
> db.movieDetails.updateMany(
    { year: {$gte: 2010, $lte: 2013}, imdb.votes": {$lt: 10000},
      $and: [{"tomato.consensus": {$exists: true} }, tomato.consensus": null} ] },
      $unset: { "tomato.consensus": "" }
    }
);
```

