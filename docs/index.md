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

Examining the distribution of ratings count marks a great starting point for the journey. The Complementary Cumulative Distribution Function is heavy-tailed, indicating that many users posted only a few ratings. Conversely, there is a small number of prolific users. This observation motivates to delve deeper into understanding the distinctions between these prolific raters and the rest of the population. Let’s pick up the experts from these figures.

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

(N.B. 95% confidence interval has not be been plot since the maximum thick of it is 0.0005)

In general, a notable pattern emerges where experts initiate the rating trend, establishing an initial inclination. As the evaluation proceeds, non-experts increasingly contribute ratings, potentially outnumbering expert assessments. This indicates that experts set the initial tone, and non-experts play a significant role by adding a larger volume of assessments as the overall trend develops.

Thus, it might be interesting to know if their ratings differ.


# What sets apart experts from non-experts ?

<iframe src="{{ site.baseurl }}/assets/plots/interactive_plot_attributes.html" width="100%" height="500" style="border: none;"></iframe>

The overall trend shows that experts assess beers more critically than non-experts. Moreover, it was remarked that experts rate beers that are less famous than beers rated by casual users. Additionally, the trends of the beers they rate are different.

<iframe src="{{ site.baseurl }}/assets/plots/interactive_plot_styles.html" width="100%" height="500" style="border: none;"></iframe>

It has been observed that experts tend to be stricter and more demanding in their ratings, which could be explained by a certain professionalism and a palate that is more sensitive to the nuances of different beer tastes. Indeed, experts are accustomed to rating all types of beers, of different styles, and especially beers that are not necessarily well-known, thus contributing to having a potentially greater impact on the success of new blockbusters. Analysing the reviews and performing a sentiment analysis highlighted that experts’ reviews are significantly less positive than casual ones. Then why should the breweries trust the experts while their perception seems to differentiate from the average consumer? It sounds paradoxical if the brewery wants to maximise its sales.

## Truly different ?

Examining mean ratings of top 16 rated styles results in the fact that experts and non experts follow the same trend over the years.

The Pale Lager style as an example, which is one of the beers with a very low average rating. Expectedly, a very low score is anticipated from most people, but a slight difference from the experts. However, over the years, it’s always a style of beer that fails to convince either experts or non-experts in any significant way. In contrast, if we take the Witbier style as an example, it's noticeable that the difference between the average score given by experts and non-experts remains very similar over the years. This trend does not restrict to the most rated beer but can be extended to the global set of beers. While a difference in their mean rating is significant, the overall behaviour of both categories are similar.

<iframe src="{{ site.baseurl }}/assets/plots/interactive_plot_beers.html" width="100%" height="500" style="border: none;"></iframe>

Taking a closer look at the different beers evaluated by experts and non-experts reveals some similarities. Indeed, the distribution of the two categories hold a certain similarity in their shape. The means of both distributions are significantly different for all the beers, due to the severity of the experts. However, the difference is seen to be very low, with a maximum absolute difference of 0.24 and an average of 0.13 ! Moreover, for 56% of beers , variances  are significantly different. Inside this percentage, the ratio of the expert standard deviation over casual one’s is always less than 1, showcasing that experts are more homogeneous. Plus, the ratio always stands above 0.75 which assesses that the differences in the variances are small. Therefore, expert and casual raters follow the same general trend.

(N.B. The proposed graph below is made upon beers over 8000 ratings but the behaviour generalises)

<iframe src="{{ site.baseurl }}/assets/plots/interactive_plot_styles_rating.html" width="100%" height="500" style="border: none;"></iframe>

In the end, experts are different, but their tendencies are similar to that of non-experts.

But why should one really care about the experts if they follow the same trend as most people who pass judgement on beers? Sure, they are tougher, but do they really add value to the analysis? Let’s take a look at the quality of their reviews to find out.

# Strong or fruity words ?

In the exploration of beer reviews, nuanced results emerge when focusing on the distinctiveness and commonality in textual reviews among experts. The divergence in linguistic patterns becomes apparent, revealing more complex and useful reviews made by the experts compared to commonplace ones.

Examining the left pint of beer, representative of expert reviews, a vocabulary more in specificity is employed, utilising refined words and adjectives that contribute to a more precise analysis. The language employed by experts confirms what is observed during this beer’s journey, reflecting on subtle nuances in flavour, aroma, and overall beer characteristics.

Conversely, the right pint of beer, symbolic of non-expert reviews, presents a contrasting narrative. The language used by non-experts tends to be more basic, lacking the finesse and precision observed in expert discourse.

<div style="text-align: center;">
  <img src="/assets/images/BeerWordCloud.png" alt="beer_words">
</div>

In addition to the examination of the linguistic nuances, focus shifts to the quantitative aspect of beer reviews by analysing the lengths of reviews provided by both experts and non-experts. There exists a significant difference in the mean lengths of reviews between the two groups, with longer reviews for casuals compared to their expert counterparts (15 additional words in average).

This nuanced understanding of both qualitative and quantitative dimensions enriches comprehension of the diverse reviewing behaviours within the beer enthusiast community.

In the context of creating a new beer, these findings bear significance. The analyses conducted by experts, characterised by their complexity and precision, emerge as a valuable resource for informed decision-making. Navigating the landscape of beer enthusiasts reveals advantages to placing greater trust in the reviews of experts, whose discerning language contributes to a more comprehensive understanding of the beer traits and pitfalls.

# Conclusion

Whether by observing the scoring or the comments left on the ratings, it is evident that experts, despite their relatively limited numbers, have a significant impact on the reputation of the beers featured on both sites. Despite their tendency to rate beers more critically than non-experts, reflecting a discerning and thoughtful perspective, they share similar traits with the other raters, indicating a corresponding behaviour. Their refined vocabulary and more accurate reviews contribute to their usefulness.

When looking at how people score and comment on beer ratings, something becomes clear: even though there aren't many experts, their opinions really matter in shaping how these beers are rated on both sites. These experts tend to be really pickier than casuals when they rate beers. It shows they are careful and thoughtful about what they're doing. However, here's the interesting fact: despite being critical, these experts are a lot like the other people who rate beers. 

What makes these experts stand out isn't just that they're really critical. The main difference lies in the difference of the vocabulary used. They employ fancy words and write clear reviews. It implies that their reviews are really helpful and easy to understand for everyone who loves beer. These experts aren't just adding their thoughts for fun, they are actually making a big difference. 

_"Stay tuned! Experts are raising a new blockbuster"_


# Ethics 

<div class="content">
  <div class="text">
    <p>
      In contemporary machine learning and applied data analysis projects like Beer Reviews Analysis, the evaluation of ethical risks is gaining importance. As designers of this kind of project, it is the responsibility to assess potential impacts and address them responsibly.
    </p>
    <p>
      Focusing specifically on the Beer Analysis, one identifiable ethical risk involves influencing consumer choices. There are both indirect stakeholders, who are impacted by the system but do not directly interact with it (including the Public, Government, or Environment), and direct stakeholders, such as admins, end-users, or contractors, who have direct interactions with the system.
    </p>
    
  </div>
  <div class="image">
    <img src="/assets/images/ethic.jpeg" alt="Ethic" width="400" height="400">
  </div>
</div>

Taking the example of influencing consumer choices, considering only direct stakeholders, which are the customers. If the dataset is used to manipulate consumer choices by promoting certain beers over others through fake reviews or biased recommendations, it can be deceptive and unethical.

In this project, the aim is to use both datasets, incorporating the maximum number of reviews possible to minimise bias in consumer reviews and recommendations. Relying on only one dataset could introduce more bias into consumer choices. Hence, incorporating both datasets serves as an additional measure to mitigate bias and provide more robust and unbiased consumer advice.







