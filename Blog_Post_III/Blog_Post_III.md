# Blog Post III

## Vision

<p align="center">
  <img src="https://lh4.googleusercontent.com/nLm1DOxktyENEu6nB5TsiuDo5p10CvaiAAWAx7QM4S5ZQFYeZYo7Xhy4ei26oCnlCpUaSprsp4yBZ-DIQhVFuG79fqm3NeOfqipz38Rb6qg3268bSLqB2YKiv6k2iA4Y7atAsIG7">
</p>

Looking back at our second pre-proposal, our vision was to find relations between freedom of expression features of a country and the listening habits of the users from those countries. We wanted to show how censorship and restrictions can affect certain activities that we take for granted like listening to music and almost streaming whatever we want whenever we want. Although our datasets had very valuable features like how many new artist did a user listen to on an average of 6 months or the amount of websites blocked by a government in a year, we did not get conclusive evidence to reject the null hypothesis that censorship does not affect listening habits. However, we know that inconclusive conclusions are still results and this has been a good project example to show that what one expects for a high confidence level is not necessarily what happens in real life.

## Data

<p align="center">
  <img src="https://lh5.googleusercontent.com/2fA6khebVU4DbvdWD1-qxVR9Ujd6w00coH_7i69-GWPQjRTdpMUO4kkoHmWIg0N5CPOauU4QxOQj_3unGEV4MeqIGgATqmqyPD3fP5yLHaIg_ADD6PYCp8mlBCKwaXpK3MA3qZgH" alt="drawing" width="400">
    <center><figcaption>Fig. 1: A visual representation of our datasets and the join we made to analyze our data</figcaption></center>
</p>

We used 3 main datasets for this project. You can look at the features that we chose to use in **[Fig. 2]**: 

1. **User Dataset:** The LFM-1b dataset **[1]** was collected by Markus Schedl and their paper that described it was published at a conference and was very useful due to the lack of user information in most music related datasets as information on a user’s country, age, etc. cannot be retrieved from, for example, Spotify, due to privacy and legal reasons. It has billions of listening events and also has additional user data that is an analysis on the listening events (novel artist listening, mainstream music listening, listening count information). We encourage you to checkout the paper that has thorough information on the dataset. (<http://www.cp.jku.at/datasets/LFM-1b/>)
2. **Internet Freedom Dataset:** For Internet freedom we used Freedom House’s 2018 dataset. Freedom House is an independent watchdog organization that is specifically analyzing freedom and democracy around the world and therefore they have a lot of information on the freedom of expression status for many countries for various years. This dataset had various information on Internet freedom such a freedom status (described by 3 classes, FREE, NOT FREE, and FREE), the amount of websites blocked, the infringements on human rights etc. You can see which ones we chose to use in **[Fig. 2]**.  (<https://freedomhouse.org/report/freedom-net/freedom-net-2018>)
3. **Press Freedom Dataset:** For press freedom we used a dataset we found on the World Bank website. This dataset has information on the press freedom index and the press freedom rank of a country. (<https://tcdata360.worldbank.org/indicators/h3f86901f?country=BRA&indicator=32416&viz=line_chart&years=2001,2015>)

<p align="center">
  <img src="https://lh5.googleusercontent.com/_bNFFbwDWcM-u1R3KmVYKTvfV8g9iPiSIb4HNQDZedRwOZMtt9L1NTRyLhYZQJAAQvQJW7PSjVeQTlmc2Oy7J1JD1CuZrKBQ8ExpOa0bDJ3bv-xJA3o4nz5IWKclEB61_x5ktrmg" alt="drawing" width="800">
    <center><figcaption>Fig. 2: The features picked and cleaned in each dataset</figcaption></center>
</p>

*(At this point, if you are looking at our code in parallel please look at* ***processing.py****)*

Our cleaning process was made so much easier thanks to the Python pandas package. Here are the modification we did for each dataset:

1. **User Dataset:** For the user dataset, we did not use the listening event dataset which was the largest part of the whole dataset. We only used the user dataset, the additional user dataset that was basically a summary of the listening events for each user. Of all of features listed in **[Fig. 2]** we only had to edit the country and the gender. For the country we wanted to equalize all datasets as our join was planned to be done on the country as seen in **[Fig. 1]**. In order to do that we used pycountry, a package that can given a name or an ISO-2 symbol give an ISO-3 symbol of the country. For the gender we simply numerized it.
2. **Internet Freedom Dataset:** For the Internet dataset we also changed the country ID to match the other datasets. Additionally we changed the “free-status” column to a numeric version of the strings with the dictionary {"NOT FREE": 0, "PARTLY FREE": 1, "FREE": 2}.
3. **Press Freedom Dataset:** The press freedom was already in ISO-3 therefore we didn’t have to change the country column. Depending on the application we either only used the freedom rank of the years 2001-2009 and 2012-2016 or the freedom index for those years. The hole in the years wasn’t our choice, it was the way the dataset was.

Finally we joined users basic information with the additional data we had on the user. We also merged the country datasets together which left us with around only 63 countries since the Internet dataset had less countries than the press freedom dataset.  

When we joined the 2 merged we were left with around 20869 rows/users. This was very satisfying in a statistical point of view. The dataset itself might have had billion of rows of listening events but there were already only enough users anyway so our lost wasn’t that big and we were satisfied with our data collection.

## Methodology

<p align="center">
  <img src="https://lh5.googleusercontent.com/mLZnsJy5OwIfKj1-9-OyZprQ2TA9KVYAbaVbdtWxWRM4sBTO7HFQYNySkgi-U-Q0GMObP29_VVpakvszqxlRROKAfkJ_mDo_9WOPqzPDyo3mIP1jgswQ8N4bSSncnwkBA6Hec3rb">
</p>

We had 3 hypotheses that we wanted to test with our data, and **as a result we used 2 ML algorithms and made 6 visualizations that also involved statistics**. We used built-in SQL-like functions of panda dataframes to join as we explained above. We also used sklearn for both of our ML algorithms: k-Means and linear regression. Finally we used matplotlib to plot all of our visualizations.

## Hypothesis & Results

### **Hypothesis 1: Relation between artist novelty and Internet freedom features**

We expect a correlation between the variety of musicians listened and the Internet freedom ranking of the country where the user is located. A country with higher ranking in freedom of Internet may have more medium to spread information about other (novel to the user) music.

<p align="center">
  <img src="https://lh4.googleusercontent.com/dMmI1L4GbJPHsZHY5ijs_Y7R8agA0btnDpyUXWsDb_DD03LeIc3nV_nz4_el0XoiyrtX8TFBtbDpxIxOdcoO_jMA8B5D-o-BgA6u9NCsW-9dDlXyj5ykHgFujgoqviK7QgiDAMID" alt="drawing" width="600">
    <center><figcaption>Fig. 3: Correlation of Novel Artist Listening and Freedom of Expression</figcaption></center>
</p>

<p align="center">
  <img src="https://lh6.googleusercontent.com/kzcUUZczCsY6tTkeu8Eo2hhq21u5kJmd1JSSjBA5x-5P37kMA-4SDQork-uK9aS2zhFLxKdD5ath72PMy2YJPSHz-r6KPTcx1PKENlNouW8IcQIM0598ZH7fVG2LbR5dBD-e5FLe" alt="drawing" width="600">
    <center><figcaption>Fig. 4: Density plot of 6m average novel artist listening count by Internet Freedom Status</figcaption></center>
</p>

### **Hypothesis 2: Relation between age /country Internet freedom features and the count of listening events**

We expect that younger generations (age 0 - 35) would find the obstacles put by the government less of a problem (ex: ease at using VPN) and have listening habits that are similar to the ones in countries. This also means that we expect the opposite from older generations.

<p align="center">
  <img src="https://lh3.googleusercontent.com/ZO1nXmXhb0fNGgMsYG3InzHng82MpQv2bOcVwfTw8mjRzNc6j4IfwB7IbsLpGQz8DcUthVWdnH5ybPvOmviI-NDZVWMlS5pwrje7WK_565ANepegqVTv_lmIPX_r6wwpegSN4X3D" alt="drawing" width="600">
    <center><figcaption>Fig. 5: Listening Count Prediction by Age (Linear Regression Plot)</figcaption></center>
</p>

<p align="center">
  <img src="https://lh4.googleusercontent.com/ySaqFxomlx5aY53YzT0i5sqcYv9CNFuLdRYZnT0JuxiILR3BuQ_ln7_IdvRLs_ByiIpdwd-8KlQy9Y7oBvbKOb0txI7it0vrx_-JdMz5tQBGpKcCOykf67AzC2kQFlGmO6n5UqF0" alt="drawing" width="600">
    <center><figcaption>Fig. 6: K-Means clusters of access block and age features</figcaption></center>
</p>

<p align="center">
  <img src="https://lh3.googleusercontent.com/XmuRdTCIOyUvH6iDvqd6hDRCFUKerPZaCYBQacTNRinuGgMOYpjbt-0Qylh8Nyq9Dz0KkkSlAMKdWYPo4jam89Sys4RhUAU7RdXwBiV7fe18qaGG4yz5STDvBIVmOugnjEvhz37K" alt="drawing" width="600">
    <center><figcaption>Fig 7: Elbow Curve of K-Means training</figcaption></center>
</p>

### **Hypothesis 3: Relation between mainstream-ness of listening and freedom of expression features** 

We expect a correlation between the number of musicians listened and the Internet freedom ranking of the country where the user is located. The motivation behind this is similar to the hypothesis above.

<p align="center">
  <img src="https://lh3.googleusercontent.com/fQRAlNVqks8vfrGFPqgEc1Xv3fLqcWq8qwG1Rtr5MbWffO-L5TzXQmMqrjrJAWBh4uqvdcNK1M8fAqOnpoDPsHXthJakXToUdi_RMPhYMbhQ9Aq38vs10dKUpOfME6Eub2iPmixa" alt="drawing" width="600">
    <center><figcaption>Fig. 8: Density of Relationship between Internet Freedom and Mainstream-ness of Listening</figcaption></center>
</p>

<p align="center">
  <img src="https://lh4.googleusercontent.com/lloZj3jDwUu8cF5prTuiDf4GfY2EQdGQivykZrlG1zGAlW0McLm2Q8OHXJj6synaO5Q19k0AjSSmdaUGn0OJRj_Y6-ElLOSTDXZmN_hoGkgWW9YYtS3P1HBD8sILX53eNWqxks5_" alt="drawing" width="600">
    <center><figcaption>Fig. 9: Density of Relationship between Press Freedom and Mainstream-ness of Listening</figcaption></center>
</p>

## Discussion of Results

**Hypothesis 1:** From the first results **[Fig. 3]**, we can conclude that the average novel artist listening count in 6 months has no correlation with any of the freedom of expression features. In order to test this further, we plotted the distribution of novel artist listening per group of country group by the freedom of Internet status **[Fig. 4]**. We showed that the means and the variances of the distributions for each internet freedom status are very similar. Thus we do not have enough evidence to refute the null hypothesis that the listening habit of novel artist listening is not related to the freedom of expression status of a country.

**Hypothesis 2:** We first made the k-means analysis and when we plotted the elbow curve **[Fig. 7]** we expected groups around 6 or so to pick up the difference of elder people living in less free countries who we hypothesized would use less VPN and therefore have less listening events, but the algorithm clearly made only differentiation on age and we had an elbow at 3 groups. When we visualized the groups in **[Fig. 6]** they were visually only categorized by age. 

We then decided to do a linear regression and predicted age by listening counts **[Fig. 5]**. Not only were the slopes not so different, but the coefficients, r-square values and p-values were very poor in the sense that we can’t even statistically confirm the accuracy of the model.

- Coefficients for "free":  [[-0.01672572]]
- R square for "free":  0.01443482701544263
- Coefficients for "partly free":  [[-0.00429118]]
- R square for "partly free":  0.0004655102677012524
- Coefficients for "not free":  [[0.00316636]]
- R square for "not free":  0.00045449493640492555

Therefore once again we weren’t able to refute the null hypothesis that listening habits are not affected by censorship.

**Hypothesis 3:** We did not find a strong enough correlation to refute the null hypothesis that mainstreaminess of a person's listening habits are unaffected by the level of media censorship in the country they live in. Our results **[Fig. 8, Fig. 9]** showed a relatively constant distribution of listening habits, independent of censorship levels. The source of this uncertainty is the lack of variation along the axis of country freedom. Because there is a relatively small amount of countries, and therefore freedom scores, even if we have a large amount of variation among user listening patterns, we are restricted when we consolidate by country due to the number of countries.

**Limitations:** after investigating a little more, we found a few reasons to explain why our results have been inconclusive conclusions.

- **Not Enough User Variety:** We can see in **[Fig. 10]** that there aren’t enough users from countries that are not free. The reasons behind this phenomenon can be that people from countries that are less free don’t have the same opportunities to express themselves on the Internet because of Internet restrictions. That makes them less likely to be users on the Last FM streaming service.
- **Not Enough Freedom Variety:** Most of the analysis we could do was around 3 types of freedom status and this lack of variety might be the reason why our ML algorithms did not pick up a relation between the features.
- **Year Mismatch:** Another reason could be that Last FM’s dataset was from 2011 while the Internet freedom dataset was from 2018 and the press freedom dataset was from a range of years. We did further investigation by making a correlation between press freedom in 2012 and still got no promising results. Therefore this is still an unclear reason.

<p align="center">
  <img src="https://lh5.googleusercontent.com/jHAorgwbk9jROksNSOPFrp4qDP1Q5DEzHJQ8k1hyV7TpPmf0rRtNakChmIIeXiXz4Cy-1W3_vHD71VLnovvMihu8hHfSjmHthwONjsP4a9WAE_CM-5cPXDFwBNRIDC3wzee32X_j" alt="drawing" width="600">
    <center><figcaption>Fig. 10: Variety of Country Internet Freedom Status in User Dataset</figcaption></center>
</p>

## Conclusion

Therefore, since we couldn’t refute any of our null hypotheses, our analysis shows there isn’t a significant relation between a country’s freedom expression and a citizen’s listening habits. We expect that this is largely due to the fact that people from countries that are less free don’t have the same Internet access because of Internet censorship. Nonetheless, this project has been an eye-opener to cases where a hypothesis might seem intuitive but there isn’t enough data to prove it.

## Additional Information

After getting inconclusive results we made some investigations between a country’s PISA score and its freedom of expression features. Once again our results were somewhat inconclusive. It seemed as if good PISA scores were obtained only if a country is extremely NOT FREE or if a country is extremely FREE. We noticed a sort of paraboloid between this density relationship but couldn’t get any information out of it and therefore decided to stick to our music dataset.

<p align="center">
  <img src="https://lh6.googleusercontent.com/EGwqT2fbhieBNLXFG6Xv8gSMpSJOnw6nlzToUVMoA_qbSQpxGYAa78Sx-R8LG1CQ6sr0UyziHSDRuG5D5qzRc4Ry2my2V81TbUhu6uyaBgDsjlci4v9RWMkgv_6yLZi-4InXRLdT" alt="drawing" width="600">
    <center><figcaption>Fig. 11: Variety of Country Internet Freedom Status in User Dataset</figcaption></center>
</p>

## References 

[1] **The LFM-1b Dataset for Music Retrieval and Recommendation**

Schedl, M.

Proceedings of the ACM International Conference on Multimedia Retrieval (ICMR 2016), New York, USA, April 2016.