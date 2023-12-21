---
layout: default
---

<!-- Text can be **bold**, _italic_, or ~~strikethrough~~. -->

Immersed in the sea of floating litres of beer within our minds, let’s plunge into the intoxicating analysis of experts and their comparison with the “everyday” beer enthusiasts. But how to define an expert among the customers? Why should truly trusting what is labelled as expertise ?

Let’s also take the example of a small local brewery that wishes to produce a new beer. In order to obtain relevant feedback, should it rather trust the public’s view or could it only rely on experts' opinion to turn its beer into an unmissable blockbuster for a Saturday night with friends.

In this flavorful journey, focus is put on analysing the reliability of expert ratings, pondering if a brewery’s destiny lies in the hands of the casual amateur drinker or in the discerned palate of insiders. Take a beer and dive in this foamy exploration, where the abundance of data unfolds the secrets of brewing success.


<div style="text-align: center;">
  <img src="/assets/images/dicaprio.png" alt="dicaprio" width="300" height="300">
</div>

# About the Dataset

The dataset consists of beer reviews collected over a period of 17 years (from 1996 to 2017) available on two websites: [BeerAdvocate](https://www.beeradvocate.com/) and [RateBeer](https://www.ratebeer.com/). The dataset contains both textual (text reviews) and numerical data (approximately 14 million ratings).

Following some analysis, the decision has been to merge the data from both platforms. This merging process aimed at obtaining more robust and meaningful results in terms of expert and non-expert ratings. It was observed that combining both datasets reduces more biases than considering each dataset separately. Considering only one or studying each of them separately would have resulted in users being experts on one website and casual users on the second, even if the user represents the same person. In order to mitigate potential biases introduced by the merge, a standardisation procedure has been implemented for the different attribute ratings that have different scales on the two websites.

As users can be registered on both websites, user ids are matched and a similar linkage process is applied to beers. This approach ensures a correct users and beers identification across the merged dataset, providing a foundation for reliable and unbiased analyses.

# Who is an expert ?

In the beer world, experts are determined by their popularity and their personal skills. As these aspects are not reflected in provided data - no personal information of users are provided - there is a need to find a proper definition of an expert.

## Distribution of the number of ratings per user

<div style="text-align: center;">
  <img src="/assets/images/CCDF.png" alt="CCDF">
</div>

Examining the distribution of ratings count marks a great starting point for the journey. The Complementary Cumulative Distribution Function is heavy-tailed, indicating that many users posted only a few ratings. Conversely, there is a small number of prolific users. This observation motivates to delve deeper into understanding the distinctions between these prolific raters and the rest of the population. Let’s pick up the experts from these figures

## Define the massive raters

In order to separate users in two groups, a definition of a massive rater, called from now an “expert” has to be found. The choice was made here to consider the number of ratings per year and aggregate scores from the past 3 years with the formula:

$$
S_{Y_j} = 2 \cdot R_{Y_{j}} + 0.5 \cdot R_{Y_{j-1}} + 0.25 \cdot R_{Y_{j-2}} + 0.1 \cdot R_{Y_{j-3}}
$$

where $$R_{Y_j}$$ denotes the number of ratings for the year $$j$$ and $$S_{Y_j}$$ is the score of the user for the year $$j$$. Therefore, the experts are people from the $$0.995$$ quantile of the score calculate previously (among those who have a non-zero score i.e. active users). These users only represent $$0.5$$% of active users, although their influence on the ratings are considerable since they account for a consequent part of the final mean rating.

## What an impact !

<div style="text-align: center;">
  <img src="/assets/images/american_pale_ale.jpg" alt="Pale Ale">
</div>

Even if experts are a minority of the active users, they represent a big part in the ratings of the beers. There are even some years and styles for which they overtake non experts. Thus, their voice really matters since they can make a huge difference for the final average rating displayed on websites. This massive influence is depicted for the style “American Pale Ale”, one of the most rated styles.

<div style="text-align: center;">
  <img src="/assets/images/mean_ratings_experts_casuals.jpg" alt="expert_prop">
</div>

In general, a notable pattern emerges where experts initiate the rating trend, establishing an initial inclination. As the evaluation proceeds, non-experts increasingly contribute ratings, potentially outnumbering expert assessments. This indicates that experts set the initial tone, and non-experts play a significant role by adding a larger volume of assessments as the overall trend develops.

Thus, it might be interesting to know if their ratings differ.

# What sets apart experts from non-experts ?

<iframe src="{{ site.baseurl }}/assets/plots/interactive_plot_attributes.html" width="100%" height="500" style="border: none;"></iframe>

The overall trend shows that experts assess beers more critically than non-experts. Moreover, it was remarked that experts rate beers that are less famous than beers rated by casual users.

A beer expert often has a more refined palate and extensive experience with various beer styles, ingredients, and brewing techniques. Their exposure allows them to detect subtle nuances, complexities, and flaws that a casual consumer might overlook. Additionally, experts may have a deeper understanding of the technical aspects of brewing, influencing their preferences and perceptions of taste. Analysing the reviews and performing a sentiment analysis showed that experts’ reviews are significantly less positive than casual ones. Then why should the breweries trust the experts while their perceptions seem to differentiate from the average consumer? It could seem paradoxical if the brewery wants to maximise its sales.


<iframe src="{{ site.baseurl }}/assets/plots/interactive_plot_styles.html" width="100%" height="500" style="border: none;"></iframe>

So far, it has been observed that experts tend to be stricter and more demanding in their ratings, which can clearly be explained by a certain professionalism and a palate that is more sensitive to the nuances of different beer tastes. Indeed, experts are accustomed to rating all types of beers, of different styles, and especially beers that are not necessarily well-known, thus contributing to having a potentially greater impact on the success of new blockbusters. So, when analyzing the opening of the brewery, there is a desire to take into account these sometimes slightly harsher and negative opinions, but which, in the long term, can certainly show all their advantages.
However, let's not forget that every expert was once a beginner and had to start at the very bottom of the ladder. That's why, when all is said and done, the question arises as to whether there aren't a few similarities in spite of everything.

## So different but so similar ?


<iframe src="{{ site.baseurl }}/assets/plots/interactive_plot_beers.html" width="100%" height="500" style="border: none;"></iframe>

<iframe src="{{ site.baseurl }}/assets/plots/interactive_plot_styles_rating.html" width="100%" height="500" style="border: none;"></iframe>


If we take a closer look at the different beers evaluated by experts and non-experts, we can still see some similarities. In fact, if we look at their distribution, we can see that despite the small bias still present between experts and non-experts, we can observe a certain similarity in the shape of the distributions. Admittedly, if we consider the number of ratings, these numbers are incomparable, but the distribution according to the years or the distribution according to the styles is quite similar for our two categories in their respective scales.

Let's just take the Pale Ale style as an example, which is one of the beers with a very low average rating. You had expect a very low score from most people, but a slight difference from the experts because of their experience and habits. However, over the years, it's always a style of beer that fails to convince either experts or non-experts in any significant way. In contrast, if we take the Witbier style as an example, we can see that the difference between the average score given by experts and non-experts remains very similar over the years. This trend is discernible for most of our styles, as well as for certain specific beers and their average rating. 

In the end, therefore, experts are different, but their tendencies are similar to that of non-experts. These observations are backed up by various interactive graphs, which clearly show this trend.

But why should one really care about the experts if they follow much the same trend as most people who pass judgment on beers? Sure, they're tougher, but do they really add value to the analysis? Let's take a look at the quality of their reviews to find out.

# Strong or fruity words ?

In our exploration of beer reviews, nuanced results emerge as we focus on the distinctiveness and commonality in textual reviews among experts. The divergence in linguistic patterns is apparent, revealing a spectrum that spans from the intricately detailed lexicon of experts to the more commonplace expressions used by non-experts.

Examining the left pint of beer, representative of expert reviews, experts employ a vocabulary more in specificity, utilizing refined words and adjectives that contribute to a more intricate and nuanced analysis. The language employed by experts confirms what is observed during this beer's journey, reflecting a depth of understanding and a penchant for articulating subtle nuances in flavor, aroma, and overall beer characteristics.

In the right pint of beer, symbolic of non-expert reviews, presents a contrasting narrative. The language used by non-experts tends to be more basic in its use of adjectives. The choice of words in non-expert reviews again lacks the finesse and precision observed in the expert discourse.

In the context of creating a new brewery, these findings bear significance. The analyses conducted by experts, characterized by their complexity and precision, emerge as a valuable resource for informed decision-making. As we navigate the landscape of beer enthusiasts, there are advantages to placing greater trust in the reviews of experts, whose discerning language contributes to a more comprehensive understanding of the beer landscape.
Conversely, the right pint of beer, symbolic of non-expert reviews, presents a contrasting narrative. The language used by non-experts tends to more basic language adjectives. The choice of words in non-expert reviews, while effective in conveying impressions, lacks the finesse and precision observed in the expert discourse.

In addition to examining the linguistic nuances, focus shifts to the quantitative aspect of beer reviews by analyzing the lengths of reviews provided by both experts and non-experts. There exists a significant difference in the mean lengths of reviews between the two groups. Furthermore, the investigation shows that non-experts tend to contribute longer reviews compared to their expert counterparts. This nuanced understanding of both qualitative and quantitative dimensions enriches comprehension of the diverse reviewing behaviors within the beer enthusiast community.

This confirms what is observed during this sparkling adventure, indicating that relying on their analysis can help improve the beer's success, even if it means involving some costs. But trust in this! It's worth it.

![BeerWordCloud](/assets/images/BeerWordCloud.png)


# Ethics 

<div class="content">
  <div class="text">
    <p>
      In contemporary machine learning and applied data analysis projects like Beer Reviews Analysis, the evaluation of ethical risks is gaining importance. As designers of this kind of project, it is the responsibility to assess potential impacts and address them responsibly.
    </p>
    <p>
      Focusing specifically on the Beer Analysis, one identifiable ethical risk involves influencing consumer choices. There are both indirect stakeholders, who are impacted by the system but do not directly interact with it (including the Public, Government, Environment, and Friends), and direct stakeholders, such as admins, end-users, or contractors, who have direct interactions with the system.
    </p>
    
  </div>
  <div class="image">
    <img src="/assets/images/ethic.jpeg" alt="Ethic" width="400" height="400">
  </div>
</div>

Taking the example of influencing consumer choices, considering only direct stakeholders, which are the customers. If the dataset is used to manipulate consumer choices by promoting certain beers over others through fake reviews or biased recommendations, it can be deceptive and unethical.

In this project, the aim is to use both datasets, incorporating the maximum number of reviews possible to minimize bias in consumer reviews and recommendations. Relying on only one dataset could introduce more bias into consumer choices. Hence, incorporating both datasets serves as an additional measure to mitigate bias and provide more robust and unbiased consumer advice.

# Conclusion





