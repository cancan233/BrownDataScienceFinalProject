# Blog Post II

## Analysis
So far in our journey to discover the relation between human listening habits and freedom of expression, we have done 3 ML analysis to test some of our hypothesis:

### **Relation between artist novelty and Internet freedom features:** 

We first investigated this relation by looking at the correlation matrix between Internet freedom features and the count of novel artists listened to by the Last FM users.  Below we presented the correlation matrix and table between different features. We found out that the only features that had a little more than zero correlation was the count of novel artists listened to in an average of 6 months. And even that feature had less than 0.05 correlation with these internet freedom features. Therefore we were not able to refute the null hypothesis the freedom of expression in a country affects the number of new artists listened to by the users.

![img](https://lh4.googleusercontent.com/7Zw2aIk1t1sGbRSyYyiuwPKx1sXVT-TgP2y1fhIbGr3ula3V9z4lri5dr-9uisbbPX0zzH-jyL-6hvxSEfu_QK7WChdoD5xU-2BMRptH8nh1hF_lAfxBl88u9QKrTz7OfKFWpUL7)

<center>*Fig. 1: Correlation Matrix Visualization*</center>

![img](https://lh6.googleusercontent.com/MmuLx5UCitbWDPCh1Z0otHTRFTtzGHNDu6kdn04AejEnVk-GeUmxstyqMwyysbZXa9f-Fipp-_EW9YbtDeJJhljxKv_5MSqsMtfYuWgiPeQRslWzjoucqXrxz_zo4oiQaL2G-GGT)

<center>*Fig. 2: Correlation Matrix Table*</center>

### **Relation between age /country Internet freedom features and the count of listening events**

Next we investigated our very first hypothesis from our blogpost by using a kMeans. For this we used scikit-learn’s kMeans algorithm to achieve the kMeans analysis. ‘Access-block’ is used to represent the internet ranking while the other features already have  their own corresponding columns. To find the optimal number of centroids, we plotted the Elbow Curve. The score is used to represent the accuracy of our model. And we see that the graph levels off rapidly after 3 clusters, implying that addition of more clusters do not improve our model but may increase the chance of overfitting.

<p align="center">
  <img src="https://lh6.googleusercontent.com/3KeqISU4YlScxNkA9DPnZeMLF4ssHH63RbFS-nLFiuw9DTHACTwABNDKJIX7clKmQMfYvK1TBQ4SJqbQnBBE_oMU2Df1FvMxas7pq_b7pPlrY8i6TOzhnWP448B6JcEbMrXxpFaO">
</p>

<center>*Fig. 3: Elbow Curve of KMeans training*</center>

After we got the optimal number of centroids, we plotted the result of kMeans using k=3. As we can see from the figure, the data points are simply categorized based upon the age of users regardless the number of ‘access block’. This potentially implies that there is no significance relationship between a user’s age, their internet accessibility and their listening habits. In other words, people are affected quite evenly by the government no matter how old they are. 

<p align="center">
  <img src="https://lh4.googleusercontent.com/cB4oPfckDIhfxgMJ2PogQ-M8lYnyydxYY9cl9Wsp4Y0oFLG6PNQvhykgl1rTiWpPWfsDnEAbUE6A7riN7z-HqAG8tWawAGX3xxDA14HrgCmPMRBxcfT-O9gH83vQ9KY0_lGflytn">
</p>

<center>*Fig. 4: Result of Kmeans(k=3)*</center>

### **Relation between mainstream-ness of listening and freedom of expression features**

In addition to the analysis we did for our midterm, we also looked at relations between freedom of expression features and the mainstream-ness of the songs listened to by the users, as it was one of our other hypothesis. When we plotted the density relationship between a country’s freedom of expression features whether it was press or Internet,  we can see that the density showed a constant line of mainstream music listening across all freedom scores. Although we expected that more popular music would be less listened to in countries with less freedom of expression because of censorship, this seems to be unvarying. Therefore once again we cannot refute the null hypothesis the mainstream-ness of the music is unaffected by the freedom of expression of the country where the listener is located.

<p align="center">
  <img src="https://lh6.googleusercontent.com/wCQZSaRqSaUBmLqKo9mxWBjO5jKSVgYf8bYl_-2tRbPVWII1KihYjxfS7gwp47JYQkC5lMelnHUfYC9xmjStLgUTQLJM2KWm7felC3K-Zka47lxJkqzdgkRDsAFk_BIg1a7EDriu">
</p>

<p align="center">
  <img src="https://lh6.googleusercontent.com/F8FDh6cv1fHK__tHiztbGn0MPUCC65JyWFQOIRGkSVODV1Wx4HFwP6NHLJ04NNp2B8dYZPKH_KLZpm4Xg5ssap9PZ28zkoud5pnNs9BONJJQWoUptNaCKK6HhDpMFcPgAC4-xIXg">
</p>

## Investigation as why we get inconclusive results

We have a few hypothesis on as to why most of our results did not reject the null hypothesis:

- **Not enough users that are from “NOT FREE” countries:**  

  When we investigated the amount of “NOT FREE” countries in our user dataset we found out that most of them were either in “PARTLY FREE” or “FREE”. In this bar chart the first bar from the left represents countries described as “NOT FREE” by the Freedom House organization, the second “PARTLY FREE” and the third “FREE”. This isn’t extremely surprising as not free countries have generally very restricted Internet access (as it’s even notable from our Internet freedom dataset.)![img](https://lh6.googleusercontent.com/c8sHJgqjA2ACI-mMFNIcAdhKme5hvQYW6m_KYHeVR9Hpk0u9ce2dkdj1NQdVaTadj8Q2KyLYcS9j5DMrKqzIPtcsXZt742v9upr_pooaMHBP60C71WI5qtF4TPTRKq8dkHrOB5hJ)

- **Year mismatch in datasets:**

  Another reason that Last FM’s dataset was from 2011 while the Internet freedom dataset was from 2018 and the press freedom dataset was from a range of years. We did further investigation by making a correlation between press freedom in 2012 and still got no promising results.

## Conclusion

We are currently doing more analysis to see if we can find any more “conclusive” results but we know that not being able to refute our hypothesis are also in a way results! We are also looking into the big listening events dataset to find more taste related results.