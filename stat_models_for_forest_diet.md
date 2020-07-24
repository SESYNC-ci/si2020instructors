# Ideas for forest diet statistical modeling 

Compiled by QDR 21 July 2020

I'll add more to this when I think of things!

## Mixed models

Also sometimes called multilevel models, mixed-effects models, or random effects models. The idea behind these models is that you have individual observations that are somehow grouped. We model the y values for those individual observations (households in your case) as if they were drawn from a distribution, where each group (cluster in your case) has its own mean. This allows us to have a higher sample size than if we just averaged each cluster and used one value per cluster, but it also accounts for the fact that households within cluster aren't statistically independent.

The R package `lme4` is probably the best package for working with multilevel models. If you want to fit Bayesian multilevel models, my favorite package is the `brms` package -- the creator of the package, Paul Bürkner, is very responsive to questions from users.

There are tons of resources about these kinds of models online. Looking through the package tutorials and vignettes is probably a good way to get started:

- [lme4 package vignette](https://cran.r-project.org/web/packages/lme4/vignettes/lmer.pdf)
- [brms package vignette](https://cran.r-project.org/web/packages/brms/vignettes/brms_overview.pdf)

Also [this book by Gelman and Hill](http://www.stat.columbia.edu/~gelman/arm/) is really great for learning about mixed models, albeit written from a Bayesian perspective. I prefer Bayesian myself but you may not want to take that approach. If not, you should try 

## Structural equation models (SEMs)

You will also hear the term path analysis (which is a specific kind of SEM), or network models or graph models (a larger family of models that includes SEMs). SEMs allow you to draw out your hypothesis about the causal relationships between variables in your system, represented by a network diagram with arrows going from cause to effect. In this model, there is not necessarily a distinction between independent and dependent (x and y) variables. A variable can be both a cause and an effect.

To me the most useful book is James Grace's book on structural equation models. It's focused on ecology applications but can be applied to other topics. [Here is a link to the book.](https://www.cambridge.org/core/books/structural-equation-modeling-and-natural-systems/D05B2328107F91AF772182F3AF88EB12) It might be a little out of date, now that it is around 10 years old, but it still has a lot of good material.

The R package `lavaan` is probably the best one for working with these kind of models. <https://lavaan.ugent.be/> It is pretty straightforward to set up and fit a SEM with the lavaan package. But it is more complicated if you want to also incorporate a multilevel random effects structure into the model. Judging from the lavaan site, it looks like it has some limited support for doing a [multilevel structural equation model](https://lavaan.ugent.be/tutorial/multilevel.html) which might be useful for you. The Bayesian alternative to the `lavaan` package is the [blavaan package](https://faculty.missouri.edu/~merklee/blavaan/).

## Conditional autoregressive models (CAR models)

This might be unnecessarily complex for your needs, but I did also want to bring these models to your attention. Another similar term you might see is spatial autoregressive (SAR) models. Those models allow you to specify a special type of random effect that accounts for the spatial orientation of the clusters relative to one another. The closer two clusters are, the less statistically independent they are. The `brms` package has this implemented in R. [This page has some cool examples](https://mc-stan.org/users/documentation/case-studies/icar_stan.html) where the different areas are different neighborhoods in NYC. (The language is a little technical but you can get an idea of the model from looking at the figures.)

## Model selection and validation

Model selection means taking multiple "candidate models" and choosing the model or models that perform the best. Usually we would want to define performance as striking the best balance between fitting the data well (describing variation in the data) but not overfitting (because then it would not be able to predict with new data points). 

For model selection with the lme4 mixed models in R, I have used the [MuMIn package](https://www.rdocumentation.org/packages/MuMIn/versions/1.43.17) in the past. It looks like there is a package that came out more recently that might have a better method for model selection with the mixed models, that I haven't used yet but I have heard of people using, the [cAIC4 package](https://arxiv.org/pdf/1803.05664.pdf).

As for model validation, I would really strongly encourage checking out the book [Introduction to Statistical Learning in R](http://faculty.marshall.usc.edu/gareth-james/ISL/) -- the book PDF is freely available. I worked through the entire book and it really explained a lot to me. It goes into some basic machine learning stuff, which you also might want to think about doing with your data.
